<template>
    <div class="container">
        <div class="row">
            <div class="col" v-for="n in 10" :key="n" >
                {{ n }}
                <p>texto</p>
                <img src="http://placekitten.com/50/50" alt="">
            </div>
        </div>
    </div>

    <br><br><br>

      <carousel :items-to-show="3">
    <slide v-for="slide in 10" :key="slide">
        <p>texto</p>
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
}
</script>

<style>
.carousel__prev--in-active,
.carousel__next--in-active {
  display: none;
}
</style>