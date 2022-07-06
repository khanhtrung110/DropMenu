<template>
  <teleport to="#dropdownModel">
    <slot></slot>
  </teleport>
</template>

<script>
import { onMounted } from "@vue/runtime-core";
export default {
  props: {
    showModel: Boolean,
  },
  setup(props, context) {
    onMounted(() => {
      const open = document.getElementById("open");
      const modal_container = document.getElementById("modal_container");
      const close = document.getElementById("close");
      modal_container.classList.add("show");
      close.addEventListener("click", () => {
        modal_container.classList.remove("show");
        context.emit("update:showModel", false);
      });
    });
  },
};
</script>

<style scope>
#open {
  display: none;
}
button {
  background-color: #47a386;
  border: 0;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  color: #fff;
  font-size: 14px;
  padding: 10px 25px;
  outline: #47a386;
}
.modal-container {
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  opacity: 0;
  pointer-events: none;
  transition: all 0.5s;
}
.modal-container.show {
  pointer-events: auto;
  opacity: 1;
}
.modal {
  background-color: #fff;
  width: 600px;
  max-width: 100%;
  border-radius: 5px;
  box-shadow: 0 2 px 4px rgba(0, 0, 0, 0.2);
  padding: 30px 50px;
  width: 600px;
  max-width: 100%;
  text-align: center;
}

.modal h1 {
  margin: 0;
}
.modal p {
  opacity: 0.7;
  font-size: 14px;
}
</style>