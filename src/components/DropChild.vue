<template>
  <div ref="optionMenu" class="select-menu">
    <div ref="selectBtn" @click="handleSelectBtn" class="select-btn">
      <span ref="sBtn_text" class="sBtn-text"
        ><i :class="imgDefault"></i>
        {{ text }}
      </span>
      <i class="fa fa-angle-down"></i>
    </div>
    <ul ref="option" class="options">
      <slot :listSelect="listSelect" :handleOption="handleOption">
        <template v-for="list in listSelect.data" :key="list.id">
          <li class="option" @click="handleOption(list)" :id="list.id">
            <span class="option-text">ss{{ list.title }}</span>
          </li>
        </template>
      </slot>
    </ul>
  </div>
</template>

<script>
import {
  reactive,
  onMounted,
  ref,
  refs,
  getCurrentInstance,
  watchEffect,
} from "@vue/runtime-core";
export default {
  props: {
    showModel: Boolean,
  },
  setup(props, context) {
    const listSelect = reactive({
      data: [
        {
          id: "alls",
          title: "all-img",
          img:"fa fa-images"
        },
        {
          id: "product",
          title: "product-images",
          img:"fa fa-ad"
        },
        {
          id: "customer",
          title: "customer-images",
          img:"fa fa-angle-double-down"
        },
        {
          id: "document",
          title: "document-images",
          img:"fab fa-algolia"
        },
        {
          id: "drberg",
          title: "dr-berg-images",
          img:"fab fa-apple"
        },
        {
          id: "food",
          title: "food-images",
          img:"fa fa-asterisk"
        },
        {
          id: "icons",
          title: "icons",
          img:"fa fa-bicycle"
        },
        {
          id: "others",
          title: "others",
          img:"fa fa-arrow-alt-circle-left"
        },
      ],
    });
    const text = ref("Select your choice");
    const imgDefault = ref("fa fa-images")
    const optionMenu = ref(null);
    const selectBtn = ref();
    const option = ref();
    const sBtn_text = ref();
    const handleSelectBtn = () => {
      optionMenu.value.classList.toggle("active");
    };
    const handleOption = (e) => {
      console.log('mlemmlem',sBtn_text.value);
      text.value = e.title;
      imgDefault.value = e.img
      if (e.id == "others") {
        context.emit("update:showModel", true);
      }
    };
    return {
      listSelect,
      optionMenu,
      selectBtn,
      option,
      sBtn_text,
      text,
      handleSelectBtn,
      handleOption,
      imgDefault
    };
  },
};
</script>

<style>
.select-menu {
  width: 380px;
  margin: 150px auto;
}
.select-menu .select-btn {
  display: flex;
  height: 55px;
  background: #fff;
  padding: 20px;
  font-size: 18px;
  font-weight: 400;
  border-radius: 8px;
  align-items: center;
  cursor: pointer;
  justify-content: space-between;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}
.select-btn i {
  font-size: 25px;
  transition: all 0.5s;
}
.sBtn-text i {
  margin-right: 10px;
}
.select-menu.active .select-btn > i {
  transform: rotate(-180deg);
}
.select-menu .options {
  position: relative;
  padding: 20px;
  margin-top: 10px;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);

  display: none;
  opacity: 0;
  transition: all 0.5s;
}
.select-menu.active .options {
  display: block;
  opacity: 1;
}
.options .option {
  display: flex;
  height: 55px;
  cursor: pointer;
  padding: 0 16px;
  border-radius: 8px;
  align-items: center;
  background: #fff;
}
.options .option:hover {
  background: #f2f2f2;
}
.option i {
  font-size: 25px;
  margin-right: 12px;
}
.option .option-text {
  font-size: 18px;
  color: #333;
}
</style>