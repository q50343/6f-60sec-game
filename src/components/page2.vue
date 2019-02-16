<template>
  <div>
    <div class="page2" v-if='this.time != 0'>
      <div class="flex pb-60">
        <div class="topLeft">
          <div class="title-2">60 SECONDS CHALLENGE</div>
          <span class="score">SCORE</span>
          <span class="score2">{{score}}</span>
        </div>
        <em class="time">00 : {{time}}</em>
      </div>
      <div class="flex">
        <span class="num">{{num}}</span>
        <span class="operator">{{operator}}</span>
        <span class="num">{{num2}}</span>
        <span class="operator">=</span>
        <input v-model="equal" class="equal" @keydown.enter="calc()">
      </div>
			<em class='press'>press enter to answer</em>
    </div>
		<final v-if='this.time == 0' :score='score' @again='again'></final>
  </div>
</template>

<script>
import final from './final'

export default {
	components:{
		final
	},
  data() {
    return {
      score: "000",
      num: 11,
      num2: 1,
      equal: "",
			time: '59',
			operator:'+'
    }
  },
  methods: {
    calc() {
			if (this.time == '00') return
			let operator = this.operator.replace(/\×/g, "*").replace(/\÷/g, "/")
			let ans = eval(`${this.num}${operator}${this.num2}`)	
		
			if (this.time > 40){
				this.equal == ans? this.score++ : this.score--
				this.num = parseInt(Math.random()*9 +1)
				this.num2 = parseInt(Math.random()*9 +1)
			}else	if (this.time > 20){
				this.equal == ans? this.score++ : this.score--
				this.num = parseInt(Math.random()*90 +10)
				this.num2 = parseInt(Math.random()*90 +10)
			}else {
				this.equal == ans? this.score = parseInt(this.score) + 5 : this.score--
				this.num = parseInt(Math.random()*900 + 100)
				this.num2 = parseInt(Math.random()*900 + 100)
			}

			this.equal = ''
			this.score = this.score.toString().padStart(3,'0')
			this.score = this.score == '0-1'? '000':this.score 
			this.operator = ['+','-','×','÷'].sort(() => {
				return Math.random() > .5? -1:1
			})[1]
		},
		again(){
      this.$emit('again')
    }
  },
  mounted() {
		this.time = 59
		this.num = parseInt(Math.random()*10)
		this.num2 = parseInt(Math.random()*10)
		document.querySelector('.equal').focus()
    let t = 59
    let time = setInterval(() => {
      t--
      if (t < 10) {
        t = "0" + t
      }
      if (t == 0) {
        clearInterval(time)
      }
      this.time = t
    }, 1000)
  }
}
</script>

<style scoped>
.title-2 {
  font-size: 30px;
  border: 4px solid #fff;
  color: #fff;
  line-height: 50px;
  padding: 0 16px;
}
.score {
  background: #fff;
  color: #ff9d00;
  width: 114px;
  text-align: center;
  margin-right: 8px;
}
.score,
.score2 {
  font-size: 30px;
  line-height: 55px;
  display: inline-block;
}
.time {
  font-size: 96px;
  color: #fff;
  font-weight: bold;
	padding-right: 4px;
}
.flex {
  display: flex;
  justify-content: space-between;
  width: 730px;
}
.num {
  font-size: 112px;
  line-height: 131px;
  width: 170px;
  text-align: center;
}
.operator {
  font-size: 92px;
  color: #fff;
  line-height: 131px;
	width: 50px;
}
.equal {
  width: 255px;
  background: #fff;
  text-align: center;
  font-size: 112px;
  line-height: 131px;
  border: none;
}
.equal:focus {
  outline: none;
}
.press{
	display: block;
	text-align: right;
	padding-right: 24px;
}
</style>
