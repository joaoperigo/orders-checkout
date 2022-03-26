<template>
    <button @click="toTop">A</button>
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