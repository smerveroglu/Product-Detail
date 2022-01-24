<template>
  <div id="app">
    <ProductDetail />
  </div>
</template>

<script>
import ProductDetail from "./components/ProductDetail.vue";

export default {
  name: "App",
  components: {
    ProductDetail,
  },
};
</script>

<style>
#app {
  background: #fff;
  font-size: 12px;
  font-weight: 400;
  color: #202020;
  font-family: Arial, Helvetica, sans-serif;
  width:1368px;
  height: 768px;
  overflow:visible;
}
</style>
