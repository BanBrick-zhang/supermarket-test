<template>
  <div id="home">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <HomeSwiper :banners="banners"></HomeSwiper>
    <HomeRecommendView :recommends="recommends"></HomeRecommendView>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import HomeSwiper from './childComps/HomeSwiper'
  import HomeRecommendView from './childComps/HomeRecommendView'
  import {getHomeMultidata} from 'network/home'

  export default {
    name: '',
    data() {
      return {
        banners:[],
        recommends: []
      }
    },
    components: {
      NavBar,
      HomeSwiper,
      HomeRecommendView
    },
    created() {
      getHomeMultidata().then(res => {
        // console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      })
    },
  }
</script>

<style scoped>
  .home-nav{
    background-color: var(--color-tint);
    color: white;
  }
</style>
