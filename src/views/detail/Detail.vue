<template>
  <div class="">
    详情页
  </div>
</template>

<script>
  export default {
    name: 'Detail',
    data() {
      return {
        Iid:null
      }
    },
    created() {
      this.Iid = this.$router.params.Iid
    },
    components: {}
  }
</script>

<style scoped>
</style>
