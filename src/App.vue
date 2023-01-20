<template>
  <div>

    <!-- <div class="start" :class="{ end: click_detail }"> -->
    <!-- <div class="start" :class="{ end: false }"> -->
    <DetailModal 
      @closeDetail="detail=false"
      :onerooms="onerooms" 
      :click_detail="click_detail" 
      :detail="detail" 
      >
    </DetailModal>

    <div class="menu">
      <a v-for="menu in menus" :key="menu">{{ menu }}</a>
    </div>

    <DiscountBanner 
      v-if="showDiscount == true" 
      :discount="discount"  
    />

    <button @click="priceSort">가격순정렬</button>
    <button @click="sortBack">되돌리기</button>

    <h3>뷰동산</h3>
    <ProductList 
      @openDetail="detail=true; click_detail=i"
      :onerooms="onerooms[i]" 
      v-for="(oneroom,i) in onerooms" :key="oneroom" 
    />

  </div>
</template>

<script>
import oneroom from './data/oneroom.js';
import DiscountBanner from './components/DiscountBanner.vue'
import DetailModal from './components/DetailModal.vue'
import ProductList from './components/ProductList.vue'

export default {
  name: 'App',
  data(){
    return{
      showDiscount: true,
      oneroomOrigin: [...oneroom],
      object: {name:'kim', age:20},
      click_detail: 0,
      detail: false,
      report: [0,0,0],
      menus: ['HOME','PRODUCT','ABOUT'],
      onerooms: oneroom, 
      discount:30,
    }
  },
  methods:{
    priceSort(){
      this.onerooms.sort(function(a,b){
        return a.price - b.price
      })
    },
    sortBack(){
      this.onerooms=[...this.oneroomOrigin];
    }
  },
  // mounted(){
  //   setTimeout(()=>{
  //     this.showDiscount=false;
  //   }, 2000)
  // },
    mounted(){
    setInterval(()=>{
      this.discount--;
      if(this.discount==0){
        this.showDiscount=false;
      }
    },1000);
  },
  components: {
    DiscountBanner: DiscountBanner,
    DetailModal: DetailModal,
    ProductList: ProductList,
  }
}
</script>

<style>
*{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
  text-align: center;
}
.start{
  opacity: 1;
  transition: all 5s;
}
.end{
  opacity: 0;
}
.fade-enter-from{
  /* transition: all 5s; */
  transition: translateY(-1000px);
}
.fade-enter-active{
  opacity:0;
}
.fade-enter-to{
  opacity:1;
}
h3{
  margin-top: 40px;
}
.menu {
  background: darkslateblue;
  padding: 15px;
}
.menu > a{
  color: white;
  margin: 10px;
}
.room_img{
  width: 100%;
  margin-top: 40px;
}
</style>
