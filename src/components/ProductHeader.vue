<template>
  <header>{{ productTitle }}</header>
</template>

<script>
export default {
  name: "ProductHeader",
  props: {
    productTitle: String,
  },
  components: {},
  data() {
    return {};
  },
  created() {},
  watch: {},
  methods: {},
};
</script>

<style>
header {
  margin-bottom: 7px;
  font-size: 20px;
  font-weight: 300;
  max-height: 49px;
  text-align: left;
  font-weight: 600;
}
</style>
