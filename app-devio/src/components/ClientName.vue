<template>
    <div class="form-group mt-4 pt-2 client-name-group">
        <label for="nome-cliente" class="w-100">
            <h1 class="text-start">Criar pedido <img class="pb-2" src="../assets/hand-pointer.svg" alt="Icone de pointer"></h1>
        </label>
        <div class="input-group mb-3" :class="{ desabilitado: isActive }" >
            <input type="text" class="form-control" placeholder="Inserir nome do cliente" aria-label="Recipient's username" aria-describedby="button-addon2" v-model="nome" id="nome-cliente">
            <button class="btn btn-devio-primary" type="button" id="button-addon2" @click="createPedido($event)">Ok</button>
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
            msg: null,
            isActive: false
        }
    },
    methods: {
    async createPedido(e) { 
        e.preventDefault()
        const data = {
            nome: this.nome,
            pedido: null,
            metodo: null,
            status: "Solicitado"
            // na verdade seria "solicitando" pois é criado quando começa o atendimento
        }
        this.isActive = true
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
h1 {
    font-weight: 300;
    text-transform: uppercase;
    cursor: pointer;
}
.form-control {
    background-color: var(--white);
    border-color: var(--dark);
    border-radius: 5px !important;
}
.form-control:focus {
    border-radius: 0;
    box-shadow: 0 0 0 0.25rem var(--tertiary);
}
button:focus {
    box-shadow: 0 0 0 0.25rem var(--tertiary);
}
.input-group {
    background-color: var(--white);
    border: solid 2px var(--primary);
    border-radius: 2px;
}
.input-group input {
    border-width: 0;
}
</style>