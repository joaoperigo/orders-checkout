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
</template>

<script>
export default {
    name: 'SliderBestSellers'
}
</script>