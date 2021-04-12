<template>
    <Swiper class="detail-seiper">
      <SwiperItem v-for="item in topImages" :key="item" class="swiper-item">
        <img :src="item" alt="">
      </SwiperItem>
    </Swiper>
</template>

<script>
  import {Swiper,SwiperItem} from 'components/common/swiper'
  export default {
    name: 'DetailSwiper',
    props:{
      topImages:{
        type:Array,
        default(){
          return []
        }
      }
    },
    data() {
      return {}
    },
    components: {
      Swiper,
      SwiperItem
    }
  }
</script>

<style scoped>
  .detail-seiper{
    height: 300px;
    overflow: hidden;
  }
</style>
