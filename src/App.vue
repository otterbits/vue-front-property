<template>

<Transition name="fade">
  <Modal @closeModal="모달창열렸니 = false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니 ="모달창열렸니" />
</Transition>

  <div class="menu">
    <a v-for="작명 in 메뉴들" :key="작명">{{ 작명 }}</a>
  </div>

  <Discount v-if="showDiscount == true"/>

  <button @click="strSort()">가나다정렬</button>
  <button @click="priceAscend()">가격오름차순정렬</button>
  <button @click="priceDescend()">가격내름차순정렬</button>
  <button @click="priceFilter()">50만원이하</button>
  <button @click="sortBack()">되돌리기</button>

  
  <Card @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(a,i) in 원룸들" :key="a"/>

</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){
    return {
      showDiscount : true,
      원룸들오리지널 : [...data],
      누른거 : 0,
      모달창열렸니 : false,
      신고수 : [0, 0, 0],
      메뉴들 : ['Home', 'Shops', 'About'],
      원룸들 : [...data],
    }
  },
  methods: {
    increase(){
      this.신고수 += 1;
    },

    strSort(){
      this.원룸들.sort(function(a,b){
        return a.title.localeCompare(b.title);
      })
    },
    
    priceAscend(){
      this.원룸들.sort(function(a,b){
        return a.price - b.price;
      })
    },

    priceDescend(){
      this.원룸들.sort(function(a,b){
        return b.price - a.price;
      })
    },

    priceFilter(){
      this.원룸들 = this.원룸들.filter((a) => a.price < 500000);
    },

    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    },
  },

  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

body {
  margin : 0
}
div {
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}


.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.close-bt {
  float: right;
  font-weight: bold;
  color: #FFFFFF;
  background: #3d8ad7;
  padding: 5px;
  border-radius: 8px;
  cursor: pointer;
}

.room-img {
  width: 100%;
  margin-top: 40px;
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
  color: white;
  padding: 10px;

}
</style>
