<template>
    <carousel :items-to-show="3">
        <slide v-for="slide in produtosDestaque" :key="slide.id">
            <p>#{{slide.id+1}} {{slide.titulo}}</p>
            <img src="http://placekitten.com/50/50" alt="">
        </slide>
        <template #addons>
        <navigation />
        <pagination />
        </template>
    </carousel>

</template>

<script>
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
export default {
    name: 'SliderBestSellers',
    components: {
    Carousel,
    Slide,
    Pagination,
    Navigation,
  },
  data() {
    return {
      produtosDestaque: null
    }
  },
  methods: {
    async getProdutos() {
    // os criterios de select poderiam ser mais elaborados no futuro, mas no momento apenas um booleano
    const req = await fetch(`http://localhost:3000/produtos/?destaque=true`)
    const data = await req.json()
    this.produtosDestaque = data
    }
  },
  mounted() {
    this.getProdutos()
  }
}
</script>

<style>
.carousel__prev--in-active,
.carousel__next--in-active {
  display: none;
}
</style>