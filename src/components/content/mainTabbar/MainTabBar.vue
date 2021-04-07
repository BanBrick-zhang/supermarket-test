<template>
  <TabBar>
      <TabBarItem path="/home" activeColor="red">
        <img slot="item-coin" src="~assets/image/tabbar/home.svg" alt="">
        <img slot="item-coin-active" src="~assets/image/tabbar/home_active.svg" alt="">
        <div slot="item-text">首页</div>
      </TabBarItem>
      <TabBarItem path="/category" activeColor="red">
        <img slot="item-coin" src="~assets/image/tabbar/category.svg" alt="">
        <img slot="item-coin-active" src="~assets/image/tabbar/category_active.svg" alt="">
        <div slot="item-text">分类</div>
      </TabBarItem>
      <TabBarItem path="/cart" activeColor="red">
        <img slot="item-coin" src="~assets/image/tabbar/shopcart.svg" alt="">
        <img slot="item-coin-active" src="~assets/image/tabbar/shopcart_active.svg" alt="">
        <div slot="item-text">购物车</div>
      </TabBarItem>
      <TabBarItem path="/profile" activeColor="red">
        <img slot="item-coin" src="~assets/image/tabbar/profile.svg" alt="">
        <img slot="item-coin-active" src="~assets/image/tabbar/profile_active.svg" alt="">
        <div slot="item-text">我的</div>
      </TabBarItem>
  </TabBar>
</template>

<script>
  import TabBar from "../../common/tabbar/TabBar";
  import TabBarItem from '../../common/tabbar/TabBarItem'
  export default {
    name: '',
    data() {
      return {}
    },
    components: {
      TabBar,
      TabBarItem
    }
  }
</script>

<style scoped>
</style>
