<template>
  
    <div id="detail">
      <DetailNavBar class="detail-navbar" @titleClick="titleClick" ref="nav"></DetailNavBar>
      <Scroll class="content" ref="scroll" :probe-type="3" @scroll="contentScroll">
        <DetailSwiper :top-images="topImages"></DetailSwiper>
        <DetailBaseInfo :goods="goods"></DetailBaseInfo>
        <DetailShopInfo :shop="shop"></DetailShopInfo>
        <DetailGoodsInfo :detail-info="detailInfo" @imageLoad="imageLoad"></DetailGoodsInfo>
        <DetailParamInfo :param-info="paramInfo" ref="params"></DetailParamInfo>
        <DetailCommentInfo :comment-info="commentInfo" ref="comment"></DetailCommentInfo>
      </Scroll>
      <DetailBottomBar @addToCart="addToCart"></DetailBottomBar>
    </div>
  
</template>

<script>
  import DetailNavBar from './childComps/DetailNavBar'
  import DetailSwiper from './childComps/DetailSwiper'
  import DetailBaseInfo from './childComps/DetailBaseInfo'
  import DetailShopInfo from './childComps/DetailShopInfo'
  import DetailGoodsInfo from './childComps/DetailGoodsInfo'
  import DetailParamInfo from './childComps/DetailParamInfo'
  import DetailCommentInfo from "./childComps/DetailCommentInfo";
  import DetailBottomBar from "./childComps/DetailBottomBar";

  import Scroll from 'components/common/scroll/Scroll'
  import {debounce} from 'common/utils'

  import {getDetail,Goods,Shop,GoodsParams} from 'network/detail';
  
  export default {
    name: 'Detail',
    data() {
      return {
        Iid:null,
        topImages:[],
        goods:{},
        detailInfo:{},
        paramInfo:{},
        commentInfo:{},
        themeTopYs:[],
        getThemeTopY:null,
        currentIndex:0
      }
    },
    created() {
      this.Iid = this.$router.params.iid

      this.getThemeTopY = debounce(() => {
        this.themeTopYs = []
        this.themeTopYs.push(0)
        this.themeTopYs.push(this.$refs.params.$el.offsetTop)
        this.themeTopYs.push(this.$refs.comment.$el.offsetTop)
      },100)

      getDetail(this.Iid).then(res => {
        const data = res.result
        // 获取顶部轮播数据
        this.topImages = data.itemInfo.topImages

        // 获取商品信息
        this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)

        // 获取店铺信息
        this.shop = new Shop(data.shopInfo)

        // 保存商品详情
        this.detailInfo = data.detailInfo

        // 获取参数信息
        this.paramsInfo = new GoodsParams(data.itemParams.info,data.itemParamsrule)

        // 获取评论数据
        if (data.rate.cRate !== 0) {
          this.commentInfo = data.rate.list[0] || {};
        }

        this.$nextTick(() => {
          //根据最新的数据，对应的dom已经被渲染，但图片还没有加载完
          // this.themeTopYs = []
          // this.themeTopYs.push(0)
          // this.themeTopYs.push(this.$refs.params.$el.offsetTop)
          // this.themeTopYs.push(this.$refs.comment.$el.offsetTop)
        })

      })
    },
    updated() {
      
    },
    components: {
      DetailNavBar,
      DetailSwiper,
      DetailBaseInfo,
      Scroll,
      DetailShopInfo,
      DetailGoodsInfo,
      DetailParamInfo,
      DetailCommentInfo,
      DetailBottomBar
    },
    mounted() {
      
    },
    methods: {
      imageLoad(){
        this.$refs.scroll.refresh()
        
      },
      titleClick(index){
        console.log(index);
        this.$refs.scroll.scrollTo(0,this.themeTopYs[0] ,300)
      },
      contentScroll(position){
        const positionY = -position.y
        let length = this.themeTopYs.length
        for(let i = 0;i < length;i++){
          if(this,currentIndex !== i &&(i < length - 1 && positionY > this.themeTopYs[i] && positionY < this.themeTopYs[i+1]) || (i === length - 1 &&positionY > this.themeTopYs)){
            this.currentIndex = i
            this.$refs.nav.currentIndex = this.currentIndex
          }
        }
      },
      addToCart(){
        const product = {}
        product.image = this.topImages[0];
        product.title = this.goods.title;
        product.desc = this.goods.desc;
        product.price = this.goods.realprice;
        product.iid = this.Iid;

        this.$store.commit
      }
    },
  }
</script>

<style scoped>
  #detail{
    position: relative;
    z-index: 9;
    background-color: #fff;
    height: 100vh;
  }
  .content{
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 49px;
  }
  .detail-navbar{
    position: relative;
    z-index: 9;
    background-color: #fff;
  }
</style>
