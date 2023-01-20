<template>
    <div>
      <img :src="onerooms.image" class="room_img">
      <h4 @click="Detail">{{ onerooms.title }}</h4>
      <p>{{ onerooms.price }}원</p>
    </div>
</template>

<script>
export default {
    name: 'ProductList',
    props: {
        onerooms: Object,
    },
    methods: {
        Detail(){
            this.$emit('openDetail',this.onerooms.id)
        },
    }
}
</script>

<style>
h4:hover{
    color: rgb(42, 137, 214);
    cursor: pointer;
}
</style>