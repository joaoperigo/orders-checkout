<template>
<MenuBar />
  <section>
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-6 offset-md-3">
            <WaitingOrders />
        </div>
      </div>
    </div>
  </section>
  <section id="secao-comprar" class="border-top mt-4">
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-6 offset-md-3">
          <ClientName @clicked="passarIdCliente" />
          <AllProductsList :idCliente="idCliente" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src
import MenuBar from '@/components/MenuBar.vue'
import WaitingOrders from '@/components/WaitingOrders.vue'
import ClientName from '@/components/ClientName.vue'
import AllProductsList from '@/components/AllProductsList.vue'

export default {
  name: 'CheckoutView',
  components: {
    MenuBar,
    WaitingOrders,
    ClientName,
    AllProductsList
  },
  data() {
        return {
          idCliente: null
        }
    },
  methods: {
      passarIdCliente (id) {
          this.idCliente = id
          // console.log(this.idCliente)
      }
  }
}
</script>

<style lang="scss" scoped>
// #secao-comprar {
//   background-color: var(--white)
// }
</style>