<template>
    <div class="container-waiting-orders">
        <h2 class="pt-3">Pedidos em espera</h2>
        <div class="accordion accordion-flush" id="accordionFlushExample">
            <div class="accordion-item">
                <h3 class="accordion-header" id="flush-headingOne">
                <button class="accordion-button d-flex justify-content-end collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#flush-collapseOne" aria-expanded="false" aria-controls="flush-collapseOne">
                    Ver lista de pedidos
                </button>
                </h3>
                <div id="flush-collapseOne" class="accordion-collapse collapse" aria-labelledby="flush-headingOne" data-bs-parent="#accordionFlushExample">
                    <div class="accordion-body">
                        <div v-for="pedidoEmEspera in pedidosEmEspera" :key="pedidoEmEspera.id">
                            {{pedidoEmEspera.nome}}
                        </div>          
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'WaitingOrders',
    data() {
        return {
            pedidosEmEspera: null
        }
    },
    methods: {
        async getPedidosEmEspera() {
        // os criterios de select poderiam ser mais elaborados no futuro, mas no momento apenas um booleano
        const req = await fetch(`http://localhost:3000/pedidos/?status=solicitado&status=produzindo`)
        const data = await req.json()
        this.pedidosEmEspera = data
        }
    },
    mounted() {
        this.getPedidosEmEspera()
    }
}
</script>

<style scoped>
.container-waiting-orders {
    border-top: 1px solid #666;
}
.accordion-item {
    border-bottom: 1px solid #666 !important;
}
.accordion-item button {
    background-color: #333;
    color: #f4f4f4;
}
.accordion-button::after {
    margin: 0 auto;
}
</style>