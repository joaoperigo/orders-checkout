<template>
    <div class="input-group mb-3 client-name">
        <input type="text" class="form-control" placeholder="Nome do cliente" aria-label="Recipient's username" aria-describedby="button-addon2" v-model="nome">
        <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="createPedido($event)">O</button>
    </div>
</template>

<script>
export default {
    name: 'ClientName',
    data() {
        return {
            nome: null
        }
    },
    methods: {
async createPedido(e) {
            e.preventDefault()

            const data = {
                nome: this.nome,
            }

            console.log(data)

            const dataJson = JSON.stringify(data)

            const req = await fetch("http://localhost:3000/pedidos", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            })

            const res = await req.json()

            // msg do sistema (colocar)

            // limpar dados (colocar)
        }
    }
    
}
</script>

<style scoped>
.client-name {
    padding-top: 100px;
}
</style>