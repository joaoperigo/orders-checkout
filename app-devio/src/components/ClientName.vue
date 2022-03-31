<template>
    <div class="form-group client-name-group">
        <label for="nome-cliente"><h2>Nome do cliente</h2></label>
        <div class="input-group mb-3">
            <input type="text" class="form-control" placeholder="Inserir nome do cliente" aria-label="Recipient's username" aria-describedby="button-addon2" v-model="nome" id="nome-cliente">
            <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="createPedido($event)">O</button>
        </div>
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
            metodo: null,
            status: "solicitado"
            // na verdade seria "solicitando" pois é criado quando começa o atendimento
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
/* .client-name-group {
    padding-top: 15px;
} */
</style>