<template>
  <div class="goods">
    <GoodsListItem v-for="item in goods" :key="item" :goodsItem="item"></GoodsListItem>
  </div>
</template>

<script>
import GoodsListItem from './GoodsListItem'


  export default {
    name: '',
    props:{
      goods:{
        type:Array,
        default(){
          return []
        }
      }
    },
    data() {
      return {}
    },
    components: {GoodsListItem}
  }
</script>

<style scoped>
  .goods{
    display: flex;
    /* 不在一行显示 */
    flex-wrap: wrap;
    /* 均等分 */
    justify-content: space-around;
  }

</style>
