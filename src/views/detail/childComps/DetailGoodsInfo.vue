<template>
  <div v-if="Object.keys(detailInfo).length !== 0" class="goods-info">
    <div class="info-desc clear-fix">
      <div class="start"></div>
      <div class="desc">{{detailInfo.desc}}</div>
      <div class="end"></div>
    </div>
    <div class="info-key">{{detailInfo.detailImage[0].key}}</div>
    <div class="info-list">
      <img v-for="(item,index) in detailInfo.detailImage[0].list" :key="index" src="item" alt="" @load="imgLoad">
    </div>
  </div>
</template>

<script>
  export default {
    name: 'DetailGoodsInfo',
    props:{
      detailInfo:{
        type:Object
      }
    },
    data() {
      return {
        counter:0,
        imagesLength:0
      }
    },
    methods: {
      imgLoad(){
        if(++this.counter === this.imagesLength){
          this.$emit('imageLoad')
        }
      }
    },
    watch:{
      detailInfo(){
        // 获取图片的个数
        this.imagesLength = this.detailInfo.detailImage[0].list.length
      }
    },
    components: {}
  }
</script>

<style scoped>
</style>
