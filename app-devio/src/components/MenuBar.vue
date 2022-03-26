<template>
    <div class="d-flex justify-content-between align-items-center menu-bar">
        <ButtonToTop />
        <ButtonPay />
    </div>
</template>

<script>
import ButtonToTop from './ButtonToTop.vue'
import ButtonPay from './ButtonPay.vue'

export default {
  name: 'MenuBar',
  components: {
    ButtonToTop,
    ButtonPay
  }
}
</script>

<style scoped>
    .menu-bar {
        position: fixed;
        z-index: 2;
        top: 0;
        left: 0;
        right: 0;
        padding: 5px 10px;
        background: #333333;
    }
</style>