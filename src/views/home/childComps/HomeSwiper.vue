<template>
  <Swiper class="home-swiper">
    <SwiperItem v-for="item in banners" :key="item.image">
      <a :href="item.link">
        <img :src="item.image" alt="" @load="ImageLoad">
      </a>
    </SwiperItem>
  </Swiper>
</template>

<script>
    import {Swiper, SwiperItem} from 'components/common/swiper';
    export default {
        name: "HomeSwiper",
        props: {
            banners:{
                type:Array,
                default() {
                    return []
                }
            }
        },
        data() {
          return {
            isLoad:false
          }
        },
        components:{
            Swiper,SwiperItem
        },
        methods: {
          ImageLoad(){
            if(!this.isLoad)
            this.$emit('swiperimageload')
            this.isLoad = true
          }
        },
    }
</script>

<style scoped>


</style>
