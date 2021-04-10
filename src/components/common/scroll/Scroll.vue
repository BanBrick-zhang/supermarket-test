<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BScroll, { PullUpLoad } from 'better-scroll'
  export default {
    name: '',
    props:{
      probeType:{
        type:Number,
        default:0
      },
      pullUpLoad:{
        type:Boolean,
        default:false
      }
    },
    data() {
      return {
        scroll:null
      }
    },
    components: {},
    mounted() {
      this.scroll = new BScroll(this.$refs.wrapper, {
        click:true,
        probeType:this.probeType,
        pullUpLoad:this.pullUpLoad
      })

      // 监听滚动坐标
      if(this.probeType === 2 || this.probeType === 3){
        this.scroll.on('scroll',(position) => {
        this.$emit('scroll',position)
        })
      }
      
      // 监听上拉加载
      if(this.pullUpLoad){
        this.scroll.on('pullingUp',() => {
          this.$emit('pullingUp')
        })
      }
      
    },
    methods: {
      scrollTo(x, y, time=600){
        this.scroll.scrollTo(x, y, 600)
      },
      finishPullUP(){
        this.scroll && this.scroll.finishPullUP()
      },
      refresh(){
        this.scroll && this.scroll.refresh()
      },
      getscrollY(){
        return this.scroll ? this.scroll.y : 0
      }
    },
  }
</script>

<style scoped>
</style>
