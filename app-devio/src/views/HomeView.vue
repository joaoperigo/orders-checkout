<template>
  <div class="container">
    <div class="row">
      <div class="col-12 col-md-6 offset-md-3">
          <MenuBar />
          <ClientName />
          <SliderBestSellers />
          <SearchBar />
          <AllProductsList />
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
  name: 'HomeView',
  components: {
    MenuBar,
    ClientName,
    SliderBestSellers,
    SearchBar,
    AllProductsList
  }
}
</script>
