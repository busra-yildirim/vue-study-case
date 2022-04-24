<template>
  <div>
    <div>{{ barem.minimumQuantity }} - {{ barem.maximumQuantity }}</div>
    <div>{{ barem.price }} {{ this.currency }}</div>
  </div>
</template>

<script>
export default {
  name: "ProductTotalPrice",
  props: {
    barem: {
      maximumQuantity: Number,
      minimumQuantity: Number,
      price: Number,
    },
    unit: Number,
  },
  components: {},
  data() {
    return {
      currency: "TL",
    };
  },
  created() {
    //console.log("barem", this.barem);
    console.log("unit - total", this.unit);
  },
  watch: {},
  methods: {},
};
</script>

<style></style>
