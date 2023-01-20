<template>
<Transition name="fade">
    <div class="black_bg" v-if="detail == true">
      <div class="white_bg">
        <h4>{{ onerooms[click_detail].title }}</h4>
        <img :src="onerooms[click_detail].image" class="room_img">
        <p>{{ onerooms[click_detail].content }}</p>
        <p>{{ onerooms[click_detail].price }}원</p>
        <input @input="total = $event.target.value">
        <!-- <input v-model="total"> -->
        <p>{{ total }}개월 선택시 금액 : {{ onerooms[click_detail].price / total }}원</p>
        <!-- <p @click="detail = false">닫기</p> -->
        <button @click="Close">닫기</button>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
    name:'DetailModal',
    data(){
      return{
        total:1,
      }
    },
    props: {
        onerooms: Array,
        click_detail: Number,
        detail: Boolean,
    },
    methods: {
        Close(){
            this.$emit('closeDetail')
        },
    },
    watch:{
      total(a){
        if(isNaN(a) == true){
          alert('숫자만 입력하세요');
          this.total="1";
        }
        if(a<0){
          alert('최소 1개월부터 가능합니다.')
          this.total="";
        }
        if(a>36){
          alert('최대 36개월까지 가능합니다.')
          this.total="";
        }
        const str=" ";
        if(a.match(str)){
          alert('공백은 치지마')
        }
        if(this.total=='2'){
        alert('누가 2개월 할부를 하래?')
        this.total="";
        }
      }
    },
    // beforeUpdate(){
    //   if(this.total=='2'){
    //     alert('누가 2개월 할부를 하래?')
    //     this.total="3";
    //   }
    // },
}
</script>

<style>
.black_bg{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 30px;
}
.white_bg{
  width: 80%;
  background: white;
  border-radius: 8px;
  padding: 35px;
}
input{
  display: block;
  margin: 0 auto;
  width: 220px;
  height: 20px;
  text-align: center;
}
button{
  display: block;
  width: 100%;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;
  font-weight: bold;
}
button:hover{
  color: orangered;
  font-weight: bold;
}
.start{
  opacity: 1;
  transition: all 5s;
}
.end{
  opacity: 0;
}
.fade-enter-from{
  transition: all 5s;
  /* transition: translateY(-1000px); */
}
.fade-enter-active{
  opacity:0;
}
.fade-enter-to{
  opacity:1;
}
</style>