<template>
  <div class="container">
    <h2>DROP DOWN</h2>

    <div class="select-box">
      <div class="options-container">
        <DropChild v-for="list in listSelect.data" :key="list.id">
          <label :for="list.id" class="option">
            <span class="option-c">
              <img src="../src/assets/hehe.png" alt="" />
              <input type="radio" class="radio" :id="list.id" name="category" />
              <label :for="list.id">{{ list.title }}</label>
            </span>
          </label>
        </DropChild>
      </div>

      <div class="selected">
        <span>
          <img src="../src/assets/hehe.png" alt="" />
          <input type="radio" class="radio" id="all" name="category" />
          <label for="all">all-img</label> </span
        ><i class="fa fa-angle-down"></i>
      </div>
    </div>

    <Modal v-if="showModel" v-model:showModel="showModel">
      <button ref="opens" id="open">Click me</button>
      <div class="modal-container" id="modal_container">
        <div class="modal">
          <h1>Modals Are You</h1>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit.
            Reprehenderit beatae illo error sapiente sunt labore quam nemo porro
            officia nisi.
          </p>
          <button id="close">Close me</button>
        </div>
      </div>
    </Modal>
  </div>
</template>
<script>
import {
  defineAsyncComponent,
  onMounted,
  reactive,
  ref,
  watchEffect,
} from "@vue/runtime-core";
import DropChild from "../src/components/DropChild";
import Loading from "../src/components/Loading"

const Modal = defineAsyncComponent({
 loader: () => import(/* webpackChunkName: "Loader" */ "./components/Modal.vue"),
 loadingComponent: Loading,
//  errorComponent: ErrorComponent,
//  delay: 3000, // delay truoc khi show loading
});



export default {
  name: "App",
  components: { DropChild, Modal },
  setup() {
    const listSelect = reactive({
      data: [
        {
          id: "alls",
          title: "all-img",
        },
        {
          id: "product",
          title: "product-images",
        },
        {
          id: "customer",
          title: "customer-images",
        },
        {
          id: "document",
          title: "document-images",
        },
        {
          id: "drberg",
          title: "dr-berg-images",
        },
        {
          id: "food",
          title: "food-images",
        },
        {
          id: "icons",
          title: "icons",
        },
        {
          id: "others",
          title: "others",
        },
      ],
    });
    const opens = ref(null);

    const showModel = ref(false);
    watchEffect(() => {
      console.log(showModel.value);
    });
    onMounted(() => {
      // ---dropdown-------
      const selected = document.querySelector(".selected");
      const optionsContainer = document.querySelector(".options-container");
      const optionsList = document.querySelectorAll(".option");
      selected.addEventListener("click", () => {
        optionsContainer.classList.toggle("active");
      });

      optionsList.forEach((o) => {
        o.addEventListener("click", () => {
          selected.querySelector("span").innerHTML = o.innerHTML;
          optionsContainer.classList.remove("active");
        });
      });
      // ------checkLastItem-------------
      let radioBtns = document.querySelectorAll("input[name='category']");
      let findSelected = async () => {
        let select = document.querySelector(
          "input[name='category']:checked"
        ).id;
        if (select == "others") {
          console.log("hehe");
          showModel.value = true;
        }
      };
      radioBtns.forEach((radioBtn) => {
        radioBtn.addEventListener("change", findSelected);
      });
    });
    return { listSelect, showModel, opens };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  box-sizing: border-box;
}
body {
  font-family: "Roboto", sans-serif;
  background: gray;
}

h2 {
  margin: 16px;
}

.container {
  margin-top: 100px;
  padding: 32px;
}

.select-box {
  display: flex;
  width: 400px;
  flex-direction: column;
}

.select-box .options-container {
  background: white;
  color: black;
  font-weight: bold;
  max-height: 0;
  width: 100%;
  opacity: 0;
  transition: all 0.4s;
  /* border-radius: 8px; */
  overflow: hidden;

  order: 1;
}

.selected {
  background-color: white;
  /* border-radius: 8px; */
  margin-bottom: 8px;
  color: black;
  font-weight: bold;
  position: relative;
  order: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.select-box .options-container.active {
  max-height: 240px;
  opacity: 1;
  overflow-y: scroll;
}

.select-box .options-container.active + .selected::after {
  transform: rotateX(180deg);
  top: -6px;
}

.select-box .options-container::-webkit-scrollbar {
  width: 8px;
  background: white;
  /* border-radius: 0 8px 8px 0; */
}

.select-box .options-container::-webkit-scrollbar-thumb {
  background: white;
  /* border-radius: 0 8px 8px 0; */
}

.select-box .option,
.selected {
  padding: 12px 24px;
  cursor: pointer;
}
.selected span {
  display: flex;
  align-items: center;
}
.option {
  display: flex;
  align-items: center;
}
img {
  width: 30px;
  height: 30px;
  margin-right: 10px;
}

.select-box .option:hover {
  background: #414b57;
  color: white;
}

.select-box label {
  cursor: pointer;
}

.radio {
  display: none;
}
.option-c {
  display: flex;
  align-items: center;
}
</style>
