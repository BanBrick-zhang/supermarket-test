<template>
  <div class="wrapper">
    <ul class="content">
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
      <li>分类</li>
    </ul>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  export default {
    name: 'CateGory',
    data() {
      return {
        scroll:null
      }
    },
    created() {
      
    },
    mounted() {
      this.scroll = new BScroll('.wrapper',{
        probeType:3,
        pullUpLoad:true
      })
      this.scroll.on('scroll',(position) => {
        // console.log(position);
      })
      this.scroll.on('pullingUp',() =>{
        console.log('上拉加载更多');
      })
    },
    
    components: {}
  }
</script>

<style scoped>
  .wrapper{
    height: 150px;
    background-color: red;

    /* 原生滚动 */
    overflow: hidden;
    /* overflow-y: scroll; */
    }
</style>
