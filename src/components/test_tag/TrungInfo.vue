<template>
<img :src="urlImage" alt="">
<p>Xin chao cac ban</p>
</template>

<script>
import { defineComponent } from "@vue/runtime-core";

export default {
     async setup(){
        const promise = new Promise((resolve, reject) =>{
            setTimeout(()=>{
                let src = 'https://images.unsplash.com/photo-1572276596237-5db2c3e16c5d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80'
                resolve(src) 
           },500);
        })
         const urlImage = await promise;
         return {urlImage}
    }
}
</script>

<style scoped>
img{
  width: 300px;
  height: 300px;
  object-fit: cover;
}

</style>