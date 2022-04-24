<template>
  <img :src="mainImage" />
</template>

<script>
export default {
  name: "ProductImage",
  props: {
    mainImage: String,
  },
  components: {},
  data() {
    return {};
  },
  created() {
    console.log("changeMainImage", this.changeMainImage);
  },
  watch: {},
  methods: {},
};
</script>

<style scoped>
img {
  flex: 1;
}
</style>
