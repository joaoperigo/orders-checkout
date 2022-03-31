<template>
{{produtosPedido}}
<!-- <form action="" @submit="pagar($event)"> -->

    <div class="accordion" id="lista-produtos">
        <div class="accordion-item" v-for="produto in produtos" :key="produto.id">

            <h2 class="accordion-header" :id="`heading${produto.id}`">
                <button class="accordion-button d-flex justify-content-between collapsed" type="button" data-bs-toggle="collapse" :data-bs-target="`#collapse${produto.id}`" aria-expanded="false" :aria-controls="`collapse${produto.id}`">
                    <img :src="produto.img" :alt="produto.alt">
                    <span>
                        #{{1+produto.id}} | {{produto.titulo}}
                    </span>
                </button>
            </h2>

            <div :id="`collapse${produto.id}`" class="accordion-collapse collapse" :aria-labelledby="`heading${produto.id}`">
                <div class="accordion-body">
                    <div class="form-group">
                        <label for="usr">QTD:</label>
                        <input type="number" id="usr" name="quantity" min="0" max="25" v-model="produto.qtd" @input="qtdProduto(produto.id, produto.qtd, produto.valor)">
                        <h1>{{produto.qtd}} | {{produto.valor}} | <span v-if="produto.qtd">{{produto.valor * produto.qtd}}</span></h1>
                    </div>
                    <div>
                        {{produto.valor}}
                    </div>
                </div>
            </div>

        </div>
    </div>

    <!-- <input type="submit" :value="this.valorTotal">

</form> -->

<button @click="pagar($event)">{{this.valorTotal}}</button>

</template>

<script>
export default {
    name: 'AllProductsList',
        props: {
        idCliente: Number
    },
    data() {
        return {
            produtos: null,
            produto_id: null,
            observacoes: null,
            qtd: null,
            selecaoProdutos: null,
            valorTotal: 0,
            produtosPedido: []
        }
    },
    methods: {
        async getProdutos() {
            // implementar busca através da barra de pesquisa, estudar se coloca aqui
            const foo = ''
            const req = await fetch(`http://localhost:3000/produtos${foo}`)
            const data = await req.json()
            this.produtos = data
        },
        async qtdProduto(index, qtd, preco) {
            this.produtosPedido = this.produtosPedido.filter(function(item) { 
                return item.id !== index;  
            });
            if(qtd>0) {
                this.produtosPedido.push({
                id: index,
                qtd: qtd,
                // titulo: titulo,
                soma: qtd*preco
                })
                this.calcValor()
            }
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
        }
    },
    mounted() {
        this.getProdutos()
    }
}
</script>