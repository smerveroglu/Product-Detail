<template>
  <div class="card">
    <div class="flex justify-content-start p-6">
      <ProductImage :data="pData"></ProductImage>
      <div class="w-7 mt-0 ml-8">
        <h1>{{ pData.productTitle }}</h1>
        <div style="color: #ffc107">
          <font-awesome-icon :icon="['fas', 'star']" />
          <font-awesome-icon :icon="['fas', 'star']" />
          <font-awesome-icon :icon="['fas', 'star']" />
          <font-awesome-icon :icon="['fas', 'star']" />
          <font-awesome-icon :icon="['fas', 'star']" />
          <a class="pl-2" style="color: #06c; outline: 0; cursor: pointer"
            >23 Yorum</a
          >
        </div>
        <div class="mt-5">
          <ins class="price"
            >{{ pData.baremList[pData.baremList.length - 1].price }}
            <span>TL </span>
            <ins class="price"
              >- {{ pData.baremList[0].price }} <span>TL</span>
            </ins>
            <span style="color: grey; font-size: 15px; font-weight: 400">
              / Adet</span
            ></ins
          >
        </div>
        <Attributes :data="pData"></Attributes>
        <UnitPrice :data="pData"></UnitPrice>
      </div>
    </div>
  </div>
</template>

<script>
import ProductImage from "../views/ProductImage.vue";
import UnitPrice from "../views/UnitPrice.vue";
import Attributes from "../views/Attributes.vue";

import productData from "../product-data.json";
export default {
  name: "ProductDetail",
  components: {
    ProductImage,
    UnitPrice,
    Attributes
  },
  data() {
    return {
      pData: productData,
      activeColor: "",
      activeSize: "",
    };
  },
  methods: {
    selectColor(value) {
      this.activeColor = value;
    },
    selectSize(value) {
      this.activeSize = value;
    },
  },
};
</script>

<style src="../styles/productDetail.scss" lang="scss"></style>
