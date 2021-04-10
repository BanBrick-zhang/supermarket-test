<template>
  <div id="home">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <TabControl @tabClick="tabClick" :titles="['流行','新款','精选']" class="tab-control-1" ref="tabControl1" v-show="isFixed"></TabControl>
    <Scroll class="content" ref="scroll" :probeType="3" :pullUpLoad="true" @scroll="contentScroll" @pullingUp="loadMore">
      <HomeSwiper :banners="banners" @swiperimageload="swiperimageload"></HomeSwiper>
      <HomeRecommendView :recommends="recommends"></HomeRecommendView>
      <HomeFeature></HomeFeature>
      <TabControl @tabClick="tabClick" :titles="['流行','新款','精选']" class="tab-control-2" ref="tabControl2"></TabControl>
      <GoodsList :goods="showGoods"></GoodsList>
      <ul>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
        <li>商品列表</li>
      </ul>
    </Scroll>
    <BackTop @click.native="backClick" v-show="isShowBackTop"></BackTop>  <!--监听组件点击添加native -->
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import TabControl from 'components/content/tabControl/TabControl'
  import GoodsList from 'components/content/goods/GoodsList'
  import Scroll from 'components/common/scroll/Scroll'
  import BackTop from 'components/content/backTop/BackTop'

  import HomeSwiper from './childComps/HomeSwiper'
  import HomeRecommendView from './childComps/HomeRecommendView'
  import HomeFeature from './childComps/HomeFeature'

  import {getHomeMultidata,getHomeGoods} from 'network/home'
  import {debounce} from 'common/utils'


  export default {
    name: '',
    data() {
      return {
        banners:[],
        recommends: [],
        goods:{
          'pop':{page:0, list:[]},
          'new':{page:0, list:[]},
          'sell':{page:0, list:[]},
        },
        currentType:'pop',
        isShowBackTop: false,
        tabOffsetTop:0,
        isFixed:false,
        saveY:0
 
      }
    },
    components: {
      NavBar,
      TabControl,
      HomeSwiper,
      HomeRecommendView,
      HomeFeature,
      TabControl,
      GoodsList,
      Scroll,
      BackTop
    },
    computed:{
      showGoods(){
        return this.goods[this.currentType].list
      }
    },
    created() {
      this.getHomeMultidata(),
      this.getHomeGoods('pop'),
      this.getHomeGoods('new'),
      this.getHomeGoods('sell')
      
    },
    mounted() {
      // 防抖动函数
      const refresh = debounce(this.$refs.scroll.refresh,200)
      // 监听item中图片加载完成
      this.$bus.$on('itemImageLoad',() => {
        refresh()
      })
    },
    destroyed() {
      
    },
    activated() {
      // 进组件
      this.$refs.scroll.scrollTo(0, this.saveY, 0)
      this.$refs.scroll.refresh()
    },
    deactivated() {
      // 离开组件
      this.saveY = this.$refs.scroll.getscrollY()
    },
    methods: {
      //事件监听
      tabClick(index){
        switch(index){
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
            break
        }
        this.$refs.tabControl1.currentIndex = index
        this.$refs.tabControl2.currentIndex = index
      },

      backClick(){
        this.$refs.scroll.scrollTo(0, 0)
      }, 
      
      contentScroll(position){
        // 判断返回顶部按钮何时出现
        this.isShowBackTop = (-position.y) > 600

        // 决定tabcontrol是否吸顶定位
        this.isFixed = (-position.y) > this.tabOffsetTop
      },
      
      loadMore(){
        this.getHomeGoods(this.currentType)
      },

      // 获取tabcontrol的offsettop的值
      swiperimageload(){
        this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop;
      },

      //网络请求
      getHomeMultidata() {
        getHomeMultidata().then(res => {
        // console.log(res);
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type){
        const page = this.goods[type].page + 1
        getHomeGoods(type,page).then(res => {
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1

          this.$refs.scroll.finishPullUP()
        })
      },

    },
  }
</script>

<style scoped>
  #home{
    /* padding-top: 44px; */
    height: 100vh;
    position: relative;
  }
  .home-nav{
    background-color: var(--color-tint);
    color: white;
/* 
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9; */
  }
  .tab-control-1{
    position: relative;
    z-index: 9;
    background-color: #fff;
  }
  /* .tab-control{
    position: sticky;
    top: 44px;
    background-color: #fff;
    z-index: 9;
  } */
  .content{
    /* height: calc(100% - 93px); */
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 49px;
  }
</style>
