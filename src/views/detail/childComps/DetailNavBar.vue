<template>
  <div id="detail">
    <NavBar>
      <div slot="left" class="back" @click="backClick">
        <img src="~assets/image/common/back.svg" alt="">
      </div>
      <div slot="center" class="title">
        <div v-for="(item, index) in titles" :key="item" class="title-item" :class="{active:index === currentIndex}" @click="titleClick(index)">{{item}}</div>
      </div>
    </NavBar>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  export default {
    name: '',
    data() {
      return {
        titles:['商品','参数','评论','推荐'],
        currentIndex:0
      }
    },
    components: {
      NavBar
    },
    methods: {
      titleClick(index){
        this.currentIndex = index
        this.$emit('titleClick',index)
      },
      backClick(){
        this.$router.back()
      }
    },
  }
</script>

<style scoped>
  .title{
    display: flex;
    font-size: 15px;
  }
  .title-item{
    flex: 1;
  }
  .active{
    color: red;
  }
  .back{
    margin-top: 8px;
  }
</style>
