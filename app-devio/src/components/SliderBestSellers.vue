<template>
  <h2 class="mt-4 pt-3 pb-3 border-top">Destaques</h2>
  <carousel :items-to-show="3.2">
      <slide v-for="slide in produtosDestaque" :key="slide.id">
        <div class="slide-best-seller">
          <img src="http://placekitten.com/100/50" alt="">
          <h3 class="">#{{slide.id+1}} {{slide.titulo}}</h3>
          <button @click="abreProduto(slide.id)" class="mx-auto btn-devio-circle">+</button>
        </div> 
      </slide>
        <!-- <template #addons>
        <navigation />
        <pagination />
        </template> -->
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
    },
    abreProduto(id) {
      // document.getElementById(`heading${id}`).scrollIntoView({
      //   behavior: 'smooth'
      // });
      // console.log(`#heading${id}`)
      let itemAcordeao = document.querySelector(`#heading${id}`)
      let topoElemento = itemAcordeao.offsetTop - 100;
      window.scroll({ top: topoElemento, behavior: "smooth" });
      let itemAcordeaoBotao = document.querySelector(`#heading${id} button`)
      if(itemAcordeaoBotao.classList.contains('collapsed')) itemAcordeaoBotao.click()
    }
  },
  mounted() {
    this.getProdutos()
  }
}
</script>

<style lang="scss">
/* .carousel__prev--in-active,
.carousel__next--in-active {
  display: none;
} */
// .slide-best-seller img {
//   // border: solid 1px var(--dark);
//   border-radius: 50%;
// }
h2 {
  font-weight: 500;
  text-transform: uppercase;
}
h3 {
  font-size: 16px;
}
</style>