<template>
    <button @click="toTop"><img src="@/assets/home.svg" alt="" class="img-fluid"></button>
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

<style lang="scss">
  button {
    border-radius: 10px;
    background-color: var(--dark);
    border: solid 1px var(--dark);
    padding: 10px 15px;
    color: var(--light);
    display: block;
    text-align: center;
  }
</style>