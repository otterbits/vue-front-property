<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
  <div class="white-bg">
    <img :src="원룸들[누른거].image" height="200px">
    <h4>{{ 원룸들[누른거].title }}</h4>
    <p>{{ 원룸들[누른거].content }}</p>
    <input v-model="month">
    <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}원</p>  
  <Discount/>
  <span class="close-bt" @click="$emit('closeModal')">닫기</span>
</div>
  </div>
</template>

<script>
import Discount from './Discount.vue';

export default {
    name : 'Modal',
    data(){
      return {
        month : 1,
      }
    },
    beforeUpdate(){
      if (this.month == 2) {
        alert('2개월은 안 받는다')
        return this.month = 3
      }
    },
    watch : {
      month(a){
        if (isNaN(a)) {
          alert('문자 입력하지 마셈')
          this.month = 1;
        }
      }
    },
    components : {
      Discount : Discount,
    },
    props : {
      원룸들 : Array,
      누른거 : Number,
      모달창열렸니 : Boolean,
    }

}
</script>

<style>

</style>