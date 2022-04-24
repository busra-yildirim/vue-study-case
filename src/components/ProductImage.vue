<template>
  <div>
    <img v-if="mainImage" :src="mainImage" />
    <div v-if="!mainImage">Ürün Stokta Yok</div>
  </div>
</template>

<script>
export default {
  name: "ProductImage",
  props: {
    mainImage: String,
    variant: Array,
  },
};
</script>

<style scoped>
img {
  flex: 1;
}
</style>
