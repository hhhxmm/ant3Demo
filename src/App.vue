<template>
  <a-button v-for="item in list" @click="onBtnClick(item)" :key="item">
    {{ item }}
  </a-button>
</template>

<script setup>
import { ref } from "vue";
import { notification } from "ant-design-vue";
const notifyParamsFormat = (params) => ({
  ...params,
  description: (h) =>
    h("div", null, [
      h("p", { domProps: { innerHTML: params.description } }, null),
    ]),
});
const keys = Object.keys(notification);
const antNotify = ref({});
keys.map((item) => {
  if (["close", "destroy", "config"].includes(item)) {
    antNotify.value[item] = notification[item];
  } else {
    antNotify.value[item] = (params) =>
      notification[item](notifyParamsFormat(params));
  }
});
const list = [
  "success",
  "error",
  "warn",
  "warning",
  "open",
  "close",
  "destroy",
];
const onBtnClick = (type) => {
  switch (type) {
    case "close":
      console.log("close");
      // this.$antNotify[type]('product-success')
      antNotify.value[type]("product-success");
      break;
    case "destroy":
      console.log("destroy");
      antNotify.value[type]();
      // this.$antNotify[type]
      break;
    default:
      console.log("default");
      // this.$antNotify[type]({
      //   message: "导入完成",
      //   description: "<div>1111</div><div>2222</div>",
      //   duration: 0,
      //   key: "product-success",
      // });
      antNotify.value[type]({
        message: "导入完成",
        description: "<div>1111</div><div>2222</div>",
        duration: 0,
        key: "product-success",
      });
      break;
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
