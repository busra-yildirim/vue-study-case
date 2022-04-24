<template>
  <div class="wrapper">
    <div v-for="i in 5" :key="i">
      <img src="https://img.icons8.com/fluency/2x/star.png" />
    </div>
    <div class="comment">23 yorum</div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
}
img {
  width: 1.5rem;
}
.comment {
  color: #309ad8;
  margin-left: 0.5rem;
}
</style>
