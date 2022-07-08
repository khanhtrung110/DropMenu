<script>
import { ref } from "@vue/reactivity"


export default ({
    setup() {
        const name = ref('')
        return {name}        
    },
})
</script>


<template>
  <div>Tab B content</div>
  <input type="text" v-model="name">
</template>