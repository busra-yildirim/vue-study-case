<template>
  <div class="image-wrapper">
    <div class="wrapper" v-if="variant.length > 0">
      <img
        :src="item"
        v-for="item in variant[0].images"
        :key="item"
        @click="selectedImage(item)"
      />
    </div>
    <div>Ürün Stokta Yok</div>
  </div>
</template>

<script>
export default {
  name: "Thumbnailler",
  props: {
    variant: Array,
  },
  mounted() {
    if (this.variant.length <= 0) {
      var element = document.getElementById("mainImage");
      element.style.display = "none";
    }
  },
  methods: {
    selectedImage(image) {
      this.$emit("image", image);
    },
  },
};
</script>

<style scoped>
.image-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
}
img {
  width: 7rem;
  height: 7rem;
  border: 1px solid #e3e3e3;
}
.image-wrapper > img {
  width: 2rem;
  height: 3rem;
  border: none;
}
.mainImage {
  display: none;
}
</style>
