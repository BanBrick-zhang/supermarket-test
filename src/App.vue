<template>
    <div id="app">
      <keep-alive exclude="DetailData">  <!--组件离开时不销毁,排除detaildata路由界面-->
        <router-view></router-view>
      </keep-alive>
      <MainTabBar></MainTabBar>
    </div>
</template>

<script>
import MainTabBar from 'components/content/mainTabbar/MainTabBar'
  export default {
    name: "App",
    components: {
      MainTabBar
    },
  };
</script>

<style>
  @import "assets/css/base.css";
</style>
