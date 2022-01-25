<template>
  <div class="w-5">
    <img :src="bigImage" />
    <div class="grid">
      <div
        class="col-12 mt-3 ml-2 cursor-pointer w-6rem"
        :class="[activeClass == index ? 'thumbnail-active' : 'thumbnail']"
        v-for="(item, index) in images"
        :key="index"
        @click="changeBigImage(item, index)"
      >
        <img :src="item" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductImage",
  props: ["data"],
  data() {
    return {
      bigImage: "",
      images: [],
      activeClass: 0,
    };
  },
  created() {
    this.bigImage = this.data.productVariants[0].images[0];
    this.data.productVariants.forEach((element) => {
      this.images.push(element.images[0]);
    });
  },
  methods: {
    changeBigImage(item, index) {
      this.activeClass = index;
      this.bigImage = item;
    },
  },
  watch: {
    "$store.state.attributes": {
      handler(newVal) {
        this.data.productVariants.forEach((element) => {
          if (
            element.attributes[1].value === newVal.renk &&
            element.attributes[0].value === newVal.beden
          ) {
            this.bigImage = element.images[0];
            this.images = element.images;
            this.$store.state.attributes.id = element.id;
          }
        });
      },
      deep: true,
    },
  },
};
</script>
<style src="../styles/productDetail.scss" lang="scss"></style>
