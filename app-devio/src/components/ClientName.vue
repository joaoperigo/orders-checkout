<template>
    <div class="form-group client-name-group mt-4 border-top pt-2">
        <label for="nome-cliente" class="w-100"><h2>Nome do cliente</h2></label>
        <div class="input-group mb-3">
            <input type="text" class="form-control me-3" placeholder="Inserir nome do cliente" aria-label="Recipient's username" aria-describedby="button-addon2" v-model="nome" id="nome-cliente">
            <button class="btn btn-dark" type="button" id="button-addon2" @click="createPedido($event)">Ok</button>
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
        this.msg = `Pedido do cliente #${ res.id },  ${ this.nome } iniciado`

        // clean msg
        setTimeout( () => this.msg = "", 3000 )

        // emite valor ao comp tela 
        this.$emit('clicked', res.id)
        }
    },
    emits: ['clicked']
}
</script>

<style lang="scss" scoped>

.form-control {
    background-color: var(--white);
    border-color: var(--dark);
    border-radius: 5px !important;
}
.btn-dark {
    border-radius: 5px !important;
}
</style>