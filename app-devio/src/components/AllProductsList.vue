<template>
{{produtoPedido}}
<form action="" @submit="pagar($event, 4)">

    <div class="item-menu" v-for="produto in produtos" :key="produto.id">
        <div class="mb-3">
            <h2>#{{1+produto.id}} | {{produto.titulo}}</h2>
            <img :src="produto.img" :alt="produto.alt">
        </div>
        <div class="form-group">
            <label for="usr">QTD:</label>
            <input type="number" id="usr" name="quantity" min="0" max="25" v-model="produto.qtd" @input="qtdProduto(produto.id, produto.qtd)">
            <h1>{{produto.qtd}} | {{produto.valor}}</h1>
        </div>
        <div>
            {{produto.valor}}
        </div>
    </div>

    <input type="submit" :value="valorTotal">

</form>

</template>

<script>
export default {
    name: 'AllProductsList',
    data() {
        return {
            produtos: null,
            produto_id: null,
            observacoes: null,
            qtd: null,
            selecaoProdutos: null,
            valorTotal: 0,
            produtoPedido: []
        }
    },
    methods: {
        async getProdutos() {
            const req = await fetch("http://localhost:3000/produtos")
            const data = await req.json()

            this.produtos = data
        },
        async qtdProduto(index, qtd) {
            this.produtoPedido = this.produtoPedido.filter(function(item) { 
                return item.id !== index;  
            });
            if(qtd>0) {
                this.produtoPedido.push({
                id: index,
                qtd: qtd
                })
            }
        },
        // async calcValor(id, valor, qtd) {
        //     this.valorTotal = for 
        // },
        async pagar(e, id) {
            e.preventDefault();
            const pedido = this.produtoPedido

            const dataJson = JSON.stringify({ pedido: pedido });

            const req = await fetch(`http://localhost:3000/pedidos/${id}`, {
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