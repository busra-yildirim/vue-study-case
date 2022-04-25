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
            : { border: '1px solid #e3e3e3' }
        "
        :class="[
          isFeatureExisted(item.name, val) ? 'is-existed' : 'is-non-existed',
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
  methods: {
    handleClick(val) {
      this.$emit("value", val);
    },
    isFeatureExisted(name, val) {
      if (name == "Beden") {
        return this.attributes.some(
          (item) => item.size == val && item.color == this.selectedColor
        );
      } else {
        return this.attributes.some(
          (item) => item.color == val && item.size == this.selectedSize
        );
      }
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
