<template>
    <div class="discount">
      <h4>지금 결제하면 {{ discount }}% 할인</h4>
    </div>
</template>

<script>
export default {
    name: 'DiscountBannner',
    data(){
      return{
       
      }
    },
    props: {
      test:String,
      test2:Number,
      discount:String,
    },
    // mounted(){
    //   setInterval(()=>{
    //     props.thiscount--;
    //   },1000);
    // }
}
</script>

<style>
    .discount{
      background: #eee;
      padding: 30px;
      margin: 10px;
      border-radius: 5px;
    }
</style>