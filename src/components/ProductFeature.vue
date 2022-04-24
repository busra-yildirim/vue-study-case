<template>
  <div class="feature-wrapper">
    <label> {{ item.name }}</label
    >:
    <div class="value-wrapper" v-for="val in item.values" :key="val">
      <div
        class="box"
        @click="handleClick(val)"
        :style="
          selectedColor == val || (existFeature && selectedSize == val)
            ? { border: '3px solid #504747' }
            : { border: '1px solid #e3e3e3' }
        "
        :class="[
          !existFeature && selectedSize == val
            ? 'is-non-existed'
            : 'is-existed',
        ]"
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
    attributes: Array,
  },
  computed: {
    filteredData() {
      let product = this.attributes.map((item) => {
        if (
          item.name == this.selectedSize &&
          item.value == this.selectedColor
        ) {
          return item;
        }
      });
      product = product.filter((item) => item != undefined);
      return product;
    },
    existFeature() {
      let isExisted;
      if (this.filteredData.length > 0) {
        isExisted = true;
      } else {
        isExisted = false;
      }
      return isExisted;
    },
  },
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
}
.is-non-existed {
  background: #f4f5f7;
  cursor: no-drop;
  border: 1px solid #e3e3e3;
}
.is-existed {
  background: #fff;
  cursor: pointer;
  border: 1px solid #e3e3e3;
}
</style>
