%<template>
    <div>
        <h1>反应测试</h1>
        <div :style="{ backgroundColor: bgColor }" class="back"  @click="swith">
          <h1 v-if="isClick && isOK" class="msg" :style="{ color: txtColor}"> 
            反应： {{ ans }} ms 
            <h2 v-if="ans < 100"> 你就是超越人类极限的存在！ </h2>
            <h2 v-if="ans >= 100 && ans < 150"> 你就是绝世反应高手！ </h2>
            <h2 v-if="ans >= 150 && ans < 170"> 职业选手都离你遥不可及！ </h2>
            <h2 v-if="ans >= 170 && ans < 200"> 你就是ZywOo! m0NESY! </h2>
            <h2 v-if="ans >= 200 && ans < 220"> 你的反应超过了90%的职业哥！ </h2>
            <h2 v-if="ans >= 220 && ans < 250"> 你这反应，职业赛场需要你！ </h2>
            <h2 v-if="ans >= 250 && ans < 300"> 你一定是FPS高手吧 </h2>
            <h2 v-if="ans >= 300 && ans < 350"> 厉害 </h2>
            <h2 v-if="ans >= 350 && ans < 400"> 正常的反应 </h2>
            <h2 v-if="ans >= 400 && ans < 450"> 大多数人的反应 </h2>
            <h2 v-if="ans >= 450 && ans < 500"> 再来一次，别失误了 </h2>
            <h2 v-if="ans >= 500 && ans < 600"> 别走神，再来一次吧 </h2>
            <h2 v-if="ans >= 600 && ans < 700"> 一定是设备不好！ </h2>
            <h2 v-if="ans >= 700 && ans < 800"> 开小差了？再来一次吧！ </h2>
            <h2 v-if="ans >= 800 && ans < 1000"> 你这喝醉了吧，再来一次吧 </h2>
            <h2 v-if="ans >= 1000 && ans < 2000"> 你这反应，基本告别FPS游戏了 </h2>
            <h2 v-if="ans >= 2000"> ??? </h2>
          </h1>
          <h1 v-if="isClick && !isOK"  class="msg" :style="{ color: txtColor}"> 太着急了，稳一点吧 </h1>
          <h1 v-if="!isClick" :style="{ color: txtColor}" class="msg"> {{ isRunning ? "等待变绿" : "点击开始" }} </h1>
          <button v-if="isClick" @click="restart" class="again"> 再来一次 </button>
        </div>
        
    </div>
</template>

<script>
export default {
  data() {
    return {
      bgColor: 'white',
      txtColor: 'black',
      isRunning: false,
      isOK: false,
      ans: 0,
      isClick: false,
      startTime: 0
    }
  },
  methods: {
    swith() { 
      this.isRunning = !this.isRunning
      if(this.isRunning && !this.isClick) {
        this.start();
      } else {
        if(!this.isClick) {
          this.click()
        }
      }
    },
    start() {
      this.bgColor = 'blue'
      this.txtColor = 'white'
      let cnt = 0;
      const intervalId = setInterval(() => {
        cnt ++
        console.log(`第 ${cnt} 秒：执行一次功能`)
        let num = Math.floor(Math.random() * 10) + 1
        if(num <= 3 && !this.isClick) {
          this.change()
          clearInterval(intervalId)
        }
        if(this.isClick) {
          clearInterval(intervalId)
        }
        if (cnt >= 15) {
          this.change()
          clearInterval(intervalId)
          console.log('执行结束')
        }
      }, 1000)
    },
    click() {
      this.isClick = true
      if(this.isOK) {
        this.ans = Date.now() - this.startTime
      } 
    },
    change() {
      this.bgColor = 'green'
      this.isOK = true
      this.startTime = Date.now()
    },
    restart() {
      this.bgColor = 'white'
      this.isRunning = false
      this.isOK = false
      this.ans = 0
      this.isClick = false
      this.startTime = 0
      this.txtColor = 'black'
    }
  }
}
</script>

<style>
.back { 
  width: 80%;
  height: 800px;
  top: 20%;
  margin: auto;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
.msg {
  padding-top: 20%;
}
.again {
  width: 100px;
  height: 40px;
  border-radius: 5px;
}
</style>
