<template>
    <nav class="d-flex align-items-center menu-bar">
        <ButtonToTop />
        <!-- <button>H</button> -->
        <ButtonPay />
    </nav>
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
        z-index: 4;
        top: 0;
        left: 0;
        right: 0;
        padding: 15px 19px;
        background: #ffffff;
        border-bottom: 2px solid #999;
    }
</style>