<template>
  <div id="app">
    <!-- 第一頁 -->
    <div class="container" v-if='!start'>
      <div class='title pb-60'>
        <h1>60</h1>
        <h2>
          <h3>SECONDS<span>+−×÷</span></h3>
          <h3>CHALLENGE</h3>
        </h2>
      </div>
      <div class="start" @click="start = true">START!</div>
      <em>try to answer more as you can</em>
    </div>
    <page2 v-if='start' @again='again'></page2>
  </div>
</template>

<script>
import page2 from './components/page2'

export default {
  components:{
    page2
  },
  data(){
    return{
      start: false
    }
  },
  methods:{
    again(){
      this.start = false
    }
  }
}
</script>

<style>
html,body{
  margin: 0;
  padding: 0;
  width: 100%;
}
*{
  box-sizing: border-box;
  font-family: 'Roboto Condensed', sans-serif;
  font-weight: bold;
}
#app{
  width: 100vw;
  height: 100vh;
  min-height: 600px;
  background: #FF9D00;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center
}
h1,h2,h3{
  margin: 0
}
h1,h2{
  display: inline-block;
}
.pb-60{
  padding-bottom: 60px;
}
h1{
  font-size: 240px;
  color:#fff;
  text-shadow: 12px 0px 0px #000;
  padding-right: 24px;
}
h3{
  font-size: 96px;
}
h3 span{
  font-size: 44px;
  color:#fff;
  line-height: 92px;
  vertical-align: top;
  border-bottom: 4px solid #fff;
  position: relative;
  margin-left:15px 
}
h3 span:after{
  content: '';
  width: 100%;
  height: 4px;
  background: #fff;
  position: absolute;
  bottom: -12px;
  left: 0;
}
.container{
  text-align: center
}
.start{
  font-size: 36px;
  color: #FF9D00;
  background: #000;
  width: 350px;
  line-height: 58px;
  cursor: pointer;
  margin: 0 auto
}
em{
  font-size: 24px;
  color: #fff;
  font-weight: normal;
}
</style>
