<template>

<form action="" @submit="sendForm($event)">

    <div class="item-menu" v-for="produto in produtos" :key="produto.id">
        <div class="mb-3">
            <h2>#{{produto.id}} | {{produto.titulo}}</h2>
            <img :src="produto.img" :alt="produto.alt">
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
            <input type="number" id="usr" name="quantity" min="1" max="5">
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
            qtd: null
        }
    },
    methods: {
        async getProdutos() {
            const req = await fetch("http://localhost:3000/produtos")
            const data = await req.json()

            this.produtos = data
        },
        sendForm(e) {
            e.preventDefault()
            const observacoes = this.observacoes 
            console.log(this.observacoes)
        }
    },
    mounted() {
        this.getProdutos()
    }
}
</script>