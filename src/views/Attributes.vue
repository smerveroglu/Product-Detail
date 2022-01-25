<template>
  <div>
    <div class="grid mt-3">
      <h3
        class="col-12 md:col-4 lg:col-3 mt-1 flex justify-content-between font-light"
      >
        {{ data.selectableAttributes[0].name }}
        <span>:</span>
      </h3>
      <div
        class="col-12 w-2"
        :class="[activeColor === value ? 'option-active' : 'option']"
        v-for="(value, index) in data.selectableAttributes[0].values"
        :key="index"
        @click="selectColor(value)"
      >
        <span>{{ value }}</span>
      </div>
    </div>
    <div class="grid mt-3">
      <h3
        class="col-12 md:col-4 lg:col-3 mt-1 flex justify-content-between font-light"
      >
        {{ data.selectableAttributes[1].name }}
        <span class="ml-8">:</span>
      </h3>
      <div
        class="col-12 w-2"
        :class="[activeSize === item.value ? 'option-active' : 'option']"
        v-for="(item, index) in size"
        :key="index"
        @click="selectSize(item.value)"
        :style="item.isPassive ? passive : {}"
      >
        <span>{{ item.value }}</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Attributes",
  props: ["data"],
  data() {
    return {
      activeColor: "",
      activeSize: "",
      size: [],
      passive: {
        pointerEvents: "none",
        background: "#f5f3f3!important",
        color: "#7a7979!important",
        borderColor: "#e4dfdd",
      },
    };
  },
  created() {
    this.size = this.data.selectableAttributes[1].values.map((item) => {
      return {
        value: item,
        isPassive: true,
      };
    });
  },
  methods: {
    selectColor(value) {
      this.activeColor = value;
      if (this.$store.state.attributes.renk !== value)
        this.$store.state.attributes.renk = value;
      let selectableSize = this.data.productVariants.flatMap((o) =>
        o.attributes[1].value === value ? [o.attributes[0].value] : []
      );
      this.size.forEach((e) => {
        if (selectableSize.includes(e.value)) {
          e.isPassive = false;
        } else {
          e.isPassive = true;
        }
      });
    },
    selectSize(value) {
      this.activeSize = value;
      if (this.$store.state.attributes.beden !== value)
        this.$store.state.attributes.beden = value;
    },
  },
};
</script>

<style src="../styles/productDetail.scss" lang="scss"></style>
