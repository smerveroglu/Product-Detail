<template>
  <div>
    <div class="grid mt-3">
      <h3 class="col-12 md:col-4 lg:col-3 -mt-1">
        {{ data.selectableAttributes[0].name }}
        <span class="ml-8">:</span>
      </h3>
      <div
        class="col-12 -mt-1 w-2"
        :class="[activeColor === value ? 'option-active' : 'option']"
        v-for="(value, index) in data.selectableAttributes[0].values"
        :key="index"
        @click="selectColor(value)"
      >
        <span>{{ value }}</span>
      </div>
    </div>
    <div class="grid mt-3">
      <h3 class="col-12 md:col-4 lg:col-3 -mt-1">
        {{ data.selectableAttributes[1].name }}
        <span class="ml-8">:</span>
      </h3>
      <div
        class="col-12 -mt-1 w-2"
        :class="[activeSize === value ? 'option-active' : 'option']"
        v-for="(value, index) in data.selectableAttributes[1].values"
        :key="index"
        @click="selectSize(value)"
      >
        <span>{{ value }}</span>
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
    };
  },
  methods: {
    selectColor(value) {
      this.activeColor = value;
      if (this.$store.state.attributes.renk !== value)
        this.$store.state.attributes.renk = value;
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
