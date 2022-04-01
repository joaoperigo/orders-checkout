<template>
    <div class="border-top container-waiting-orders">
        <!-- <h2 class="pt-2">Pedidos em espera</h2> -->
        <div class="accordion accordion-flush mt-4" id="accordionFlushExample">
            <div class="accordion-item">
                <h2 class="accordion-header" id="flush-headingOne">
                    <button class="accordion-button d-flex justify-content-center collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#flush-collapseOne" aria-expanded="false" aria-controls="flush-collapseOne">
                        Ver lista de pedidos
                    </button>
                </h2>
                <div id="flush-collapseOne" class="accordion-collapse collapse" aria-labelledby="flush-headingOne" data-bs-parent="#accordionFlushExample">
                    <div class="accordion-body mx-2">
                        <div v-if="this.pedidosEmEspera!=''">
                            <div v-for="pedidoEmEspera in pedidosEmEspera" :key="pedidoEmEspera.id" class="d-flex justify-content-between border-bottom">
                                <div class="text-start w-50">{{pedidoEmEspera.nome}}</div> 
                                <div class="text-end w-50">{{pedidoEmEspera.status}}</div>
                            </div>
                        </div>
                        <div v-else>
                            Nenhum pedido ainda
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
            pedidosEmEspera: ''
        }
    },
    methods: {
        async getPedidosEmEspera() {
        // os criterios de select poderiam ser mais elaborados no futuro, mas no momento apenas um booleano
        const req = await fetch(`http://localhost:3000/pedidos/?status=Solicitado&status=Produzindo`)
        const data = await req.json()
        this.pedidosEmEspera = data
        }
    },
    mounted() {
        this.getPedidosEmEspera()
    }
}
</script>

<style lang="scss" scoped>

// .container-waiting-orders {
//     border-top: 1px solid var(--neutral);
// }
.accordion-item {
    background-color: transparent;
}
.accordion-body {
    background-color: var(--white);
    color: --dark;
    border-radius: 0 0 5px 5px ;
    border: 1px solid var(--neutral);
    border-top-width: 0;
}
.accordion-flush .accordion-item .accordion-button {
    border-radius: 10px;
    //reset bootstrap
    font-size: unset;
    font-weight: 500;
    color: var(--dark);
    text-transform: uppercase;
}
// .accordion-item .show{
//     border: 1px solid #666 !important;
//     border-top-width: 0 !important;
// }
.accordion-item button {
    background-color: var(--secondary);
    color: --white;
    // border: --dark solid 1px;
    text-align: center;
}
.accordion-button:focus {
    box-shadow: 0 0 0 0.25rem var(--tertiary);
}
// .accordion-button::after {
//     // margin: 0 auto;
//     // background-image: url(@/assets/relogio.svg);
// }
.accordion-button:not(.collapsed) {
    color: unset;
    background-color: var(--secondary);
}
</style>