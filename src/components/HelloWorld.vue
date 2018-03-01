<template>
  <div class="hello">
    <input type="text" v-model="userName">
    <!--<ul class="bg-bubbles">-->
      <!--<li v-for="i in 10" :key="i"></li>-->
    <!--</ul>-->
    <span v-for="i in text" v-bind:key="i.index" style="display:block">{{i}}</span>
    <input type="text" v-model="word">
    <button @click="submit()">submit</button>
  </div>

</template>

<script>
import io from 'socket.io-client';

const socket = io('http://35.201.218.18:1337');

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      text:　['default:init'],
      word: '123',
      userName: ''
    }
  },
  mounted() {
    this.init();
    this.listen();
  },
  methods: {
    init() {
      socket.connect('http://35.201.218.18:1337');
    },
    listen() {
      socket.on('jack', data =>{
          console.log(data);
          this.text.push(data.userName + ':' + data.word);
      })
    },
    submit() {
      let data = {
        userName: this.userName,
        word: this.word
      }
      socket.emit('jack',data);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  .bg-bubbles {
    position: absolute;
    background: linear-gradient(to bottom right, #50A3A2, #53E3A6);
  // 使气泡背景充满整个屏幕；
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  li {
    position: absolute;
  // bottom 的设置是为了营造出气泡从页面底部冒出的效果；
    bottom: -160px;
  // 默认的气泡大小；
    width: 40px;
    height: 40px;
    background-color: rgba(255, 255, 255, 0.15);
    list-style: none;
  // 使用自定义动画使气泡渐现、上升和翻滚；
  animation: square 15s infinite;
    transition-timing-function: linear;
  // 分别设置每个气泡不同的位置、大小、透明度和速度，以显得有层次感；
      &:nth-child(1) {
       left: 10%;
       border-radius: 20px;
     }
  &:nth-child(2) {
     left: 20%;
     width: 90px;
     height: 90px;
     border-radius: 45px;
     animation-delay: 2s;
     animation-duration: 7s;
   }
  &:nth-child(3) {
     left: 25%;
     animation-delay: 4s;
    border-radius: 20px;
   }
  &:nth-child(4) {
     left: 40%;
     width: 60px;
    border-radius: 30px;
     height: 60px;
     animation-duration: 8s;
     background-color: rgba(255, 255, 255, 0.3);
   }
  &:nth-child(5) {
     left: 70%;
    border-radius: 20px;
   }
  &:nth-child(6) {
     left: 80%;
     width: 120px;
     height: 120px;
    border-radius: 60px;
     animation-delay: 3s;
     background-color: rgba(255, 255, 255, 0.2);
   }
  &:nth-child(7) {
     left: 32%;
     width: 160px;
     height: 160px;
    border-radius: 80px;
     animation-delay: 2s;
   }
  &:nth-child(8) {
     left: 55%;
     width: 20px;
     height: 20px;
    border-radius: 10px;
     animation-delay: 4s;
     animation-duration: 15s;
   }
  &:nth-child(9) {
     left: 25%;
     width: 10px;
     height: 10px;
    border-radius: 5px;
     animation-delay: 2s;
     animation-duration: 12s;
     background-color: rgba(255, 255, 255, 0.3);
   }
  &:nth-child(10) {
     left: 85%;
     width: 160px;
     height: 160px;
    border-radius: 80px;
     animation-delay: 5s;
   }
  }
  // 自定义 square 动画；
  @keyframes square {
    0% {
      opacity: 0.5;
      transform: translateY(0px) rotate(45deg);
    }
    25% {
      opacity: 0.75;
      transform: translateY(-400px) rotate(90deg)
    }
    50% {
      opacity: 1;
      transform: translateY(-600px) rotate(135deg);
    }
    100% {
      opacity: 0;
      transform: translateY(-1000px) rotate(180deg);
    }
  }
  }
  .hello {
    background: linear-gradient(to bottom right, #50A3A2, #53E3A6);
  }
</style>
