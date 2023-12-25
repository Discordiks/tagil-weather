<template>
  <div class="title">
    <img src="@/assets/img/image 1.png" alt="">
    <h1>{{title}}</h1>
  </div>
</template>

<script>
export default {
    name: 'TitleBlock',
    data(){
        return{

        }
    },
    props:['title']
}
</script>

<style>
.title{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap:50px;
}
.title h1{
    font-size: 56px; 
}
</style>