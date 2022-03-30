<template>
  <div class="container">
    <div class="row">
      <div class="col-12 col-md-6 offset-md-3">
          <MenuBar />
          <ClientName @clicked="onClickChild" />
          <SliderBestSellers />
          <SearchBar />
          <AllProductsList :idCliente="idCliente" />
          <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import MenuBar from '@/components/MenuBar.vue'
import ClientName from '@/components/ClientName.vue'
import SliderBestSellers from '@/components/SliderBestSellers.vue'
import SearchBar from '@/components/SearchBar.vue'
import AllProductsList from '@/components/AllProductsList.vue'

export default {
  name: 'CheckoutView',
  components: {
    MenuBar,
    ClientName,
    SliderBestSellers,
    SearchBar,
    AllProductsList
  },
  data() {
        return {
          idCliente: null
        }
    },
  methods: {
      onClickChild (id) {
          this.idCliente = id
          console.log(this.idCliente)
      }
  }
}
</script>
