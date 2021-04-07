<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive">
      <slot name="item-coin"></slot>
    </div>
    <div v-else>
      <slot name="item-coin-active"></slot>
    </div>
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TabBarItem',
    props:{
      path:String,
      activeColor: {
        type:String,
        defalut:'red'
      }
    },
    data() {
       return {
        //  isActive: false
       }
    },
    computed:{
      isActive(){
        return !this.$route.path.indexOf(this.path)
      },
      activeStyle(){
        return this.isActive ? {color:this.activeColor} : {}
      }
    },
    methods: {
      itemClick(){
        this.$router.replace(this.path)
      }
    },
    components: {}
  }
</script>

<style scoped>
  .tab-bar-item{
    flex: 1;
    text-align: center;
    height: 49px;
  }
  .tab-bar-item img{
    widows: 24px;
    height: 24px;
    margin-top: 3px;
    margin-bottom: 2px;
    vertical-align: middle;
  }

</style>
