<template>

  <h2>DROP DOWN</h2>
  <DropChild v-slot="dropProps" v-model:showModel="showModel">
    <template v-for="list in dropProps.listSelect.data" :key="list.id">
      <li class="option" @click="dropProps.handleOption(list)" :id="list.id">
        <i :class="list.img"></i>
        <span class="option-text">{{ list.title }}</span>
      </li>
    </template>
  </DropChild>
  <Modal v-if="showModel" v-slot="{handelModelContainer}"  v-model:showModel="showModel" >
     <div class="modal">
          <h1>Modals Are You</h1>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit.
            Reprehenderit beatae illo error sapiente sunt labore quam nemo porro
            officia nisi.
          </p>
          <button @click="handelModelContainer" ref="btnClose" id="close">Close me</button>
      </div>
  </Modal>
    <div v-if="error">
       Error loading component {{error}}
    </div>
    <transition name="fade">
   <Suspense>
    <template #default>
      <TrungInfo/>
    </template>
    <template #fallback>
     <p>Loading...</p>
    </template>
  </Suspense>
  </transition>
</template>
<script>
import {
  defineAsyncComponent,
  onErrorCaptured,
  onMounted,
  reactive,
  ref,
  watchEffect,
} from "@vue/runtime-core";
import DropChild from "../src/components/DropChild";
import Loading from "../src/components/Loading";
import ErrorComponent from "../src/components/Loading";
import TrungInfo from "../src/components/test_tag/TrungInfo";
import CompA from "../src/components/test_tag/CompA";
import CompB from "../src/components/test_tag/CompB";

const Modal = defineAsyncComponent({
  loader: () =>
    import(/* webpackChunkName: "Loader" */ "./components/Modal.vue"),
  loadingComponent: Loading,
  errorComponent: ErrorComponent,
  //  delay: 3000, // delay truoc khi show loading
});

export default {
  name: "App",
  components: { DropChild, Modal, TrungInfo,CompA,CompB},
  setup() {
    const opens = ref(null);
    const showModel = ref(false);
    const error = ref(null);
    const showP = ref(false);
    onErrorCaptured(e => {
      error.value = e;
      return true;
    })
    onMounted(() => {});
    return { 
     showModel,
     opens,
     error,
     showP,
     };
  },
};
</script >

<style>
#app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
*{
  box-sizing: border-box;
}
body {
  background-color: #e3f2fd;
}
img{
  width: 300px;
  height: 300px;
  object-fit: cover;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-to{
  opacity: 1;
}
.fade-enter-active{
  transition: all 2s ease;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-to{
  opacity: 0;
}
.fade-leave-active{
  transition: all 2s ease;
}


</style>
