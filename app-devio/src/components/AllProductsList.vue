<template>
{{produtosPedido}}
<form action="" @submit="pagar($event, 4)">

    <div class="accordion" id="lista-produtos">
        <div class="accordion-item" v-for="produto in produtos" :key="produto.id">

            <h2 class="accordion-header" :id="`heading${produto.id}`">
                <button class="accordion-button" type="button" data-bs-toggle="collapse" :data-bs-target="`#collapse${produto.id}`" aria-expanded="true" :aria-controls="`collapse${produto.id}`">
                    <span>
                        #{{1+produto.id}} | {{produto.titulo}}
                    </span>
                    <img :src="produto.img" :alt="produto.alt">
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

    <input type="submit" :value="idCliente">

</form>

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
                soma: qtd*preco
                })
            }
        },
        // async calcValor(id, valor, qtd) {
        //     this.valorTotal = for 
        // },
        async pagar(e, id) {
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