<template>
  <div>
    <div class="barem mt-2 grid">
      <div class="col-4 mt-2">
        <h3 class="md:col-4 lg:col3 -mt-1 w-5">
          Toptan Fiyat
          <span>:</span>
        </h3>

        <h3 class="-mt-4 md:col-4 lg:col-3">(Adet)</h3>
      </div>
      <div class="col-8 mt-4">
        <div class="grid -ml-7">
          <div
            class="w-4"
            v-for="(value, index) in data.baremList"
            :key="index"
          >
            <div
              class="border-right-2 w-5"
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
              class="border-right-2 w-5"
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
      <div class="col-4 mt-2">
        <h3 class="-mt-4 md:col-4 lg:col-3">
          Adet
          <span>:</span>
        </h3>
      </div>
      <div class="col-8">
        <div class="grid -ml-7 -mt-3">
          <input class="w-4rem h-2rem mr-3" type="number" v-model="unit" />
          <p style="color: grey; font-size: 15px">Adet</p>
        </div>
      </div>
    </div>
    <div class="col-12">
      <div class="grid mt-1">
        <h2 class="w-4rem h-2rem mr-3 font-semibold">Toplam</h2>
        <h1 class="mt-2 ml-6 font-bold">: {{ totalPrice }} TL</h1>
      </div>
    </div>
    <button class="font-bold">SEPETE EKLE</button>
  </div>
</template>
<script>
export default {
  name: "UnitPrice",
  props: ["data"],
  data() {
    return {
      unit: null,
      activeClass: -1,
      totalPrice: 0,
    };
  },
  watch: {
    unit: {
      handler(newVal) {
        this.data.baremList.forEach((element, index) => {
          if (
            newVal >= element.minimumQuantity &&
            newVal <= element.maximumQuantity
          ) {
            this.totalPrice = newVal * element.price;
            this.activeClass = index;
          }
        });
        if (newVal < this.data.baremList[0].minimumQuantity) {
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
