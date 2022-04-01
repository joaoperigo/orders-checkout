<template>
    <SliderBestSellers />
    <SearchBar @clicouBusca="passarValorBusca" />
    <form action="" @click="pagar($event)" class="pt-4">

        <div class="accordion" id="lista-produtos">
            <div class="accordion-item mb-4" v-for="produto in produtos" :key="produto.id">

                <h2 class="accordion-header" :id="`heading${produto.id}`">
                    <button class="accordion-button d-flex justify-content-between collapsed" type="button" data-bs-toggle="collapse" :data-bs-target="`#collapse${produto.id}`" aria-expanded="false" :aria-controls="`collapse${produto.id}`">
                        <img class="img-produto" :src="produto.img" :alt="produto.alt">
                        <h2 class="mx-auto">
                            #{{1+produto.id}} | {{produto.titulo}}
                        </h2>
                    </button>
                </h2>

                <div :id="`collapse${produto.id}`" class="accordion-collapse collapse" :aria-labelledby="`heading${produto.id}`">
                    <div class="accordion-body">
                            <div class="row">
                                <div class="col">
                                    <div class="mb-3">
                                        <label class="form-label">Quantidade
                                            <input type="number" class="form-control text-center" name="quantity" min="0" max="25" v-model="produto.qtd" @input="qtdProduto(produto.id, produto.qtd, produto.valor, produto.titulo, produto.observacoes)" placeholder="0">
                                        </label>
                                    </div>
                                </div>
                                <div class="col">
                                    <div class="display-valores">
                                        <div><b>Valor:</b> </div>
                                        <div>{{produto.valor}}</div>
                                    </div>
                                    <div class="display-valores">
                                        <div><b>Qtd x Valor:</b> </div>
                                        <div>
                                            <span v-if="produto.qtd">{{produto.valor * produto.qtd}}</span>
                                            <span v-else>0</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="mt-4 form-floating" v-show="false">
                                <textarea class="form-control" placeholder="Leave a comment here" :id="`floatingTextarea${produto.id}`" style="height: 100px" v-model="produto.observacoes" @input="observacoesProduto(produto.id, produto.observacoes)"></textarea>
                                <label :for="`floatingTextarea${produto.id}`">Observações</label>
                            </div>
                    </div>
                </div>

            </div>
        </div>
        <div class="text-center wrapper-button-pay" v-show="this.valorTotal!=0">
            <input type="submit" class="mx-auto button-pay" :value="`Pagar: R$${valorTotal}`">
        </div>
    </form>
</template>

<script>
import SliderBestSellers from '@/components/SliderBestSellers.vue'

import SearchBar from './SearchBar.vue'

export default {
    name: 'AllProductsList',
        props: {
        idCliente: Number
    },
    components: {
        SearchBar,
        SliderBestSellers
    },
    data() {
        return {
            produtos: null,
            // produto_id: null, //devia ter usado como foreign key 
            tituloProduto: null,
            observacoes: null,
            qtd: null,
            selecaoProdutos: null,
            valorTotal: 0,
            produtosPedido: [],
            valorBusca: ''
        }
    },
    methods: {
        async getProdutos() {
            const req = await fetch(`http://localhost:3000/produtos/${this.valorBusca}`)
            const data = await req.json()
            this.produtos = data
        },
        async qtdProduto(index, qtd, preco, titulo, observacoes) {
            this.produtosPedido = this.produtosPedido.filter(function(item) { 
                return item.id !== index;  
            });
            if(qtd>0) {
                let auxObservacoes =''
                if(observacoes) auxObservacoes = observacoes
                this.produtosPedido.push({
                    id: index,
                    qtd: qtd,
                    tituloProduto: titulo,
                    soma: qtd*preco,
                    observacoes: auxObservacoes
                })
                this.calcValor()
            }
        },
        async observacoesProduto(index, observacoes) {
            console.log(observacoes)
        },
        async calcValor() {
            this.valorTotal = this.produtosPedido.map(conta => conta.soma).reduce((acc, soma) => soma + acc);
        },
        async pagar(e) {
            e.preventDefault();
            const pedido = this.produtosPedido

            const dataJson = JSON.stringify({ pedido: pedido });

            const req = await fetch(`http://localhost:3000/pedidos/${this.idCliente}`, {
            method: "PATCH",
            headers: { "Content-Type": "application/json" },
            body: dataJson
            });

            const res = await req.json();    
        },
        passarValorBusca (vB) {
            let checaTipo = /^\d+$/.test(vB)
            if(checaTipo) this.valorBusca = `?id=${vB}`
            else if(checaTipo=='') this.valorBusca = ''
            else this.valorBusca = `?titulo=${vB}`
            this.getProdutos()
            console.log(this.valorBusca)
        }
    },
    mounted() {
        this.getProdutos()
    },
    computed: {
        recebeObservacoes() {
            return this.observacoes
        }
    }
}
</script>


<style lang="scss" scoped>
    // * {
    //     background-color: transparent;
    //     border-width: 0;
    //     outline: none;
    // }
    .wrapper-button-pay {
        position: fixed;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        z-index: 4;
        padding-top: 15px;
    }
    .button-pay {
        // position: absolute;
        // top: 50%;
        // left: 50%;
        // transform: translateY(-50%) translateX(-50%);
        border-radius: 10px;
        background-color: var(--primary);
        border: 0;
        padding: 10px 15px;
        color: var(--light);
    }
    .accordion-item {
        background-color: transparent;
        border: 1px solid var(--dark);
        border-radius: 10px;
    }
    // .accordion-item:first-of-type .accordion-button  {
    //     border-top-left-radius: 10px;
    //     border-top-right-radius: 10px;
    // }
    .accordion-button {
        background-color: var(--primary);
        border-radius: 10px !important;
    }
    // .accordion-collapse {
    //     border-bottom-left-radius: 10px;
    //     border-bottom-right-radius: 10px;
    //     border: 1px solid var(--dark);
    //     border-top-width: 0;
    // }
    .accordion-button:focus {
        border-color: var(--primary);
        box-shadow: 0 0 0 0.25rem var(--tertiary);
        border-radius: 10px;
    }
    input:focus {
        box-shadow: 0 0 0 0.25rem var(--tertiary);
    }
    // .display-valores {
    //     border: solid 1px var(--primary)
    // }
    .img-produto {
        border-radius: 50%;
    }
    h2 {
        font-size: 20px;
        color: var(--light)
    }
</style>