<template>
  <div>
    <Tetris></Tetris>
  </div>
</template>

<script>
import Tetris from './components/Tetris.vue'
export default {
  name:'App',
  components:{
    Tetris
  }
}
</script>

<style lang="less" scoped>
  *{
    margin: 0;
    padding: 0;
  }
</style>