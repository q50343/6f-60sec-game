<template>
    <div>
        <div class="title">60 SECONDS CHALLENGE</div>
        <h4>YOUR FINAL SCORE</h4>
        <div class="score">{{parseInt(score)}}</div>
        <div class="start" @click="again">TRY AGAIN!</div>
    </div>
</template>

<script>
export default {
    props:['score'],
    methods:{
        again(){
            this.$emit('again')
        }
    }
}
</script>

<style scoped>
.title{
  font-size: 30px;
  border: 4px solid #fff;
  color: #fff;
  line-height: 50px;
  padding: 0 16px;
  width: 348px;
  margin: 0 auto
}
h4{
    font-size: 56px;
    margin: 10px;
    position: relative;
}
h4::before,h4::after{
    content: '';
    width: 25px;
    height: 6px;
    position: absolute;
    background: #fff;
    top:calc(50% - 3px);
}
h4::before{
    left: -40px;
}
h4::after{
    right: -40px;
}
.score{
    font-size: 112px;
    text-align: center;
}
.start{
    margin-top: 90px;
    text-align: center;
}
</style>
