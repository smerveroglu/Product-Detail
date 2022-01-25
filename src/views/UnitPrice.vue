<template>
  <div>
    <div class="barem mt-2 grid">
      <div class="col-3 mt-2 flex flex-column">
        <h3 class="flex justify-content-between font-light">
          Toptan Fiyat
          <span>:</span>
        </h3>

        <h3 class="mt-1 font-light">(Adet)</h3>
      </div>
      <div class="col-9 mt-4">
        <div class="grid">
          <div
            class="w-4"
            v-for="(value, index) in data.baremList"
            :key="index"
          >
            <div
              class="border-right-1 w-5"
              :class="[activeClass === index ? 'yellowBarem' : 'barem']"
              v-if="index !== data.baremList.length - 1"
            >
              <span>
                {{ value.minimumQuantity }} - {{ value.maximumQuantity }}</span
              >
              <div>
                <span>{{ value.price }} TL</span>
              </div>
            </div>

            <div
              class="border-right-1 w-5"
              :class="[activeClass === index ? 'yellowBarem' : 'barem']"
              v-else
            >
              <span>{{ value.minimumQuantity }} +</span>
              <div>
                <span>{{ value.price }} TL</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-3 mt-1">
        <h3 class="flex justify-content-between font-light">
          Adet
          <span>:</span>
        </h3>
      </div>
      <div class="col-9 flex flex-row align-items-center">
        <input class="w-4rem h-2rem mr-3" type="number" v-model="unit" />
        <p style="color: grey; font-size: 15px">Adet</p>
      </div>
    </div>
    <div class="grid mt-2">
      <h2 class="col-12 md:col-4 lg:col-3 mt-1 flex justify-content-between">
        Toplam
        <span>:</span>
      </h2>
      <div class="col-12 w-4 -mt-3">
        <h1 class="font-bold">{{ totalPrice }} TL</h1>
      </div>
    </div>

    <button class="font-bold" @click="addItem()" :disabled="isEmpty">
      SEPETE EKLE
    </button>
  </div>
</template>
<script>
export default {
  name: "UnitPrice",
  props: ["data"],
  data() {
    return {
      unit: "",
      activeClass: -1,
      totalPrice: 0,
      barem: {},
    };
  },
  computed: {
    isEmpty() {
      return (
        Object.values(this.$store.state.attributes).every(
          (value) => value === ""
        ) || this.activeClass === -1
      );
    },
  },
  methods: {
    addItem() {
      console.log(
        "id: ",
        this.$store.state.attributes.id,
        "barem: ",
        this.barem
      );
    },
  },
  watch: {
    unit: {
      handler(newVal) {
        this.data.baremList.forEach((element, index) => {
          if (
            newVal >= element.minimumQuantity &&
            newVal <= element.maximumQuantity
          ) {
            this.barem = element;
            this.totalPrice = newVal * element.price;
            this.activeClass = index;
          }
        });
        if (
          newVal < this.data.baremList[0].minimumQuantity ||
          newVal >
            this.data.baremList[this.data.baremList.length - 1].maximumQuantity
        ) {
          this.activeClass = -1;
          this.totalPrice = 0;
        }
      },
      deep: true,
    },
  },
};
</script>

<style src="../styles/productDetail.scss" lang="scss"></style>
