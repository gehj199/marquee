<template>
  <div id="app">
    <Carousel :imgData="imgData" :timeSpan="timeSpan" />
    <span>跑马灯结束</span>
  </div>
</template>

<script>
import Carousel from './components/Carousel'

export default {
  name: 'App',
  data:function(){
    return {
      imgData:[{url:require('@/assets/images/s1.png'),link:'/home'},
            {url:require('@/assets/images/s2.png'),link:'/num'},
            {url:require('@/assets/images/s3.png'),link:'/echart'},
            {url:require('@/assets/images/s4.png'),link:'/radio'}],
        timeSpan:3000
    }
  },
  components: {
    Carousel //轮播图组件
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
