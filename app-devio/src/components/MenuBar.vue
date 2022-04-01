<template>
    <nav class="d-flex align-items-center border-bottom menu-bar">
        <div class="container">
          <div class="row">
            <div class="col-12 col-md-6 offset-md-3">
              <ButtonToTop />
            </div>
          </div>
        </div>
    </nav>
</template>

<script>
import ButtonToTop from './ButtonToTop.vue'

export default {
  name: 'MenuBar',
  components: {
    ButtonToTop
  },
  props: {
    botaoValorTotal: Number
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
        background: var(--white);
        /* border-bottom: 1px solid var(--neutral); */
    }
</style>