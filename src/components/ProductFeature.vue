<template>
  <div class="feature-wrapper">
    <label> {{ item.name }}</label
    >:
    <div class="value-wrapper" v-for="val in item.values" :key="val">
      <div
        class="box"
        @click="handleClick(val)"
        :style="
          selectedColor == val || selectedSize == val
            ? { border: '3px solid #504747' }
            : { border: none }
        "
      >
        {{ val }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductFeature",
  props: {
    item: {
      name: String,
      values: Array,
    },
    selectedColor: String,
    selectedSize: String,
  },
  components: {},
  data() {
    return {};
  },
  created() {
    console.log("item featur", this.item);
    console.log("selectedColor22", this.selectedColor);
  },
  watch: {},
  methods: {
    handleClick(val) {
      this.$emit("value", val);
    },
  },
};
</script>

<style>
.feature-wrapper {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.feature-wrapper > label {
  width: 4rem;
}
.value-wrapper {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.box {
  width: 7rem;
  height: 3rem;
  line-height: 3rem;
  padding: 0;
  border: 1px solid #e3e3e3;
  cursor: pointer;
}
</style>
