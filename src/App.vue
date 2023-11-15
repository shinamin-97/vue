<template>
  
  <transition name="fade">
    <Modal @closeModal="modalopen = false" 
    :onerooms= "onerooms" 
    :clicknow = "clicknow" 
    :modalopen = "modalopen"/>
  </transition>

  <div class="menu">
    <a v-for="i in menu" :key="i">{{i}}</a>
  </div>

  <Discount v-if="showDiscount == true" @cas="showDiscount = false"/>



  <button @click="priceSort">가격순정렬</button>
  <button @click="repriceSort">가격역순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="modalopen = true; clicknow = i" :oneroom="onerooms[i]" v-for="(a,i) in onerooms" :key="i"/>



</template>

<script>

import data from './oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';


export default {
  name: 'App',
  data(){
    return{
      showDiscount : true,
      oneroomsOrigin : [...data],
      Object : {name : 'kim', age : 20},
      clicknow : 0,
      onerooms : data,
      modalopen : false,
      report : [0,0,0],
      menu : ['Home', 'Shop', 'About'],
      products : ['역삼동 원룸', '천호동 원룸', '마포구 원룸'],

    }
  },

  methods : {
    increase() {
      this.report[0] +=1;
    },
    sortBack() {
     this.onerooms = [...this.oneroomsOrigin];
    },
    priceSort() {
      this.onerooms.sort(function(a,b){
        return a.price - b.price;
      })
    },
    repriceSort() {
      this.onerooms.sort(function(a,b){
        return b.price - a.price;
      })
    },

  },

  // watch:{
  //     amount(a){
  //       if(a < 1){
  //         this.showDiscount == false;
  //       }
  //     }
  //   },

  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
}

}
</script>

<style>

.fade-enter-from{
  opacity: 0;
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  opacity: 1;
}

.fade-leave-from{
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color : white;
  padding: 10px;
}

.room-img{
  width: 100%;
  margin-top: 40px;
}

body {
  margin: 0;
}

div{
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg{
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}

.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

</style>
