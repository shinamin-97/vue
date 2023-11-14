<template>
  <div class="black-bg" v-if="modalopen == true">
    <div class="white-bg">
      <img :src ="onerooms[clicknow].image" style="width: 100%;">
      <h4>{{onerooms[clicknow].title}}</h4>
      <p>{{onerooms[clicknow].content}}</p>
      <input v-model="month">
      <p> {{month}}개월 선택함 : {{onerooms[clicknow].price * month}}원</p>
      <button @click="close">닫기</button>
    </div>
  </div>
  </template>
  
  
  
  <script>
  export default {
      name: 'Modal',
      data() {
        return{
            month : 1,
        }
      },
      watch : {
        month(a){
            if(a >= 13) {
                alert("13개월 이상은 불가능 합니다.")
                this.month = 1
            } else if(isNaN(a) == true){
                alert("숫자만 입력하세요");
                this.month = 1;
            }
        }
      },
      props : {
        onerooms : Array,
        clicknow : Number,
        modalopen : Object,
      },
      methods : {
        close() {
            this.$emit('closeModal')
        }
      }
      
  }
  
  </script>
  
  <style>
  
  </style>