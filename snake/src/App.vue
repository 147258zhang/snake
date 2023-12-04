<template>
  <div>
    <Snake></Snake>
  </div>
</template>

<script>
import Snake from './components/Snake.vue'
export default {
  name:'App',
  components:{
    Snake
  }
}
</script>

<style lang="less" scoped>
  *{
    margin: 0;
    padding: 0;
  }
</style>