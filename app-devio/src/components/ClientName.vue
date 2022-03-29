<template>
    <div class="input-group mb-3 client-name">
        <input type="text" class="form-control" placeholder="Nome do cliente" aria-label="Recipient's username" aria-describedby="button-addon2" v-model="nome">
        <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="createPedido($event)">O</button>
    </div>
    <Message :msg="msg" v-show="msg" />
</template>

<script>
import Message from './Message.vue'
export default {
    name: 'ClientName',
      components: {
    Message
    },
    data() {
        return {
            nome: null,
            msg: null
        }
    },
    methods: {
    async createPedido(e) { 
        e.preventDefault()

        const data = {
            nome: this.nome,
            pedido: null,
            metodo: null
        }

        console.log(data)

        const dataJson = JSON.stringify(data)

        const req = await fetch("http://localhost:3000/pedidos", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: dataJson
        })

        const res = await req.json()

        // msg from system
        this.msg = `Pedido do liente #${ res.id },  ${ this.nome } iniciado`

        // clean msg
        setTimeout( () => this.msg = "", 3000 )

        // emite valor ao comp tela 
        this.$emit('clicked', res.id)
        }
    },
    emits: ['clicked']
}
</script>

<style scoped>
.client-name {
    padding-top: 100px;
}
</style>