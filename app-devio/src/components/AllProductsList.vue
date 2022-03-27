<template>

<form action="">

    <div class="item-menu" v-for="produto in produtos" :key="produto.id">
        <div class="mb-3">
            <h2>#{{produto.id}} | {{produto.titulo}}</h2>
            <img :src="produto.img" :alt="produto.alt">
            <button class="adicionar-produto" @click="addProduto($event)">+</button>
        </div>
        <div class="mb-3">
            <label for="observacoes" class="form-label">Email address</label>
            <div class="form-floating">
                <textarea class="form-control" placeholder="Leave a comment here" id="floatingTextarea" v-model="observacoes"></textarea>
                <label for="floatingTextarea">Observações</label>
            </div>
        </div>
        <div class="form-group">
            <label for="usr">QTD:</label>
            <input type="number" id="usr" name="quantity" min="0" max="25">
        </div>
    </div>

    <input type="submit" value="Pagar">

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
            selecaoProdutos: null
        }
    },
    methods: {
        async getProdutos() {
            const req = await fetch("http://localhost:3000/produtos")
            const data = await req.json()

            this.produtos = data
        },
        async addProduto(e) {
            e.preventDefault()
            this.selecaoProdutos =  [{
                    id: 1,
                    titulo: "Macarrão",
                    observacoes: "Sem Maionese",
                    qtd: 2
                },
                {
                    id: 2,
                    titulo: "Coca-Cola",
                    observacoes: "Gelo limão",
                    qtd: 2
                }]          
        }
    },
    mounted() {
        this.getProdutos()
    }
}
</script>