<template>
    <button @click="toTop" class="btn-devio-dark"><img src="@/assets/home.svg" alt="" class="img-fluid"></button>
</template>

<script>
export default {
    name: 'ButtonToTop',
    
    methods: {
      toTop: function () {
        window.scrollTo({
          top: 0,
          behavior: "smooth"
        });
      },
    },
}
</script>

<style lang="scss" scoped>
.btn-devio-dark img {
  width: 30px;
  height: auto;
}
</style>