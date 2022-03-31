<template>
    <div class="accordion accordion-flush" id="accordionFlushExample">
        <div class="accordion-item">
            <h2 class="accordion-header" id="flush-headingOne">
            <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#flush-collapseOne" aria-expanded="false" aria-controls="flush-collapseOne">
                Pedidos em espera
            </button>
            </h2>
            <div id="flush-collapseOne" class="accordion-collapse collapse" aria-labelledby="flush-headingOne" data-bs-parent="#accordionFlushExample">
                <div class="accordion-body">
                    <div v-for="pedidoEmEspera in pedidosEmEspera" :key="pedidoEmEspera.id">
                        {{pedidoEmEspera.nome}}
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