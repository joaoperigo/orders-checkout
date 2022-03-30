<template>
<div id="pedido-table">
    <Message :msg="msg" v-show="msg" />
    <div>
      <div id="pedido-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente: </div>
        <div>Pedido: </div>
        <div>Qtd: </div>
      </div>
    </div>
    <div id="pedido-table-rows">
      <div class="pedido-table-row" v-for="pedido in pedidos" :key="pedido.id">
        <div class="order-number">{{pedido.id}}</div>
        <div>{{pedido.nome}}</div>
        <div v-for="lista in pedido.pedido" :key="lista.id">
            {{lista.qtd}} x titulo{{lista.id}}
        </div>
        <div>
          <select name="status" class="status" @change="updatedPedido($event, pedido.id)">
            <option value="">Selecione </option>
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="pedido.status == s.tipo">{{ s.tipo }}</option>
          </select>
          <button class="delete-btn" @click="deletePedido(pedido.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Message from '@/components/Message.vue'
  export default {
    name: "CozinhaView",
    data() {
      return {
        pedidos: null,
        pedido_id: null,
        status: [],
        msg: null
      }
    },
    components: {
      Message
    },
    methods: {
      async getPedidos() {
        const req = await fetch("http://localhost:3000/pedidos")
        const data = await req.json();
        this.pedidos = data;
        // rescue status
        this.getStatus();
      },
      async getListapedido() {
        const req = await fetch("http://localhost:3000/pedidos?id=5")
        const data = await req.json();
        this.pedidos = data;
        console.log(data)
      },
      async getStatus() {
        const req = await fetch("http://localhost:3000/status");
        const data = await req.json();
        this.status =data;
        this.status = data;
        console.log(data);
      },
      async deletePedido(id) {
        const req = await fetch(`http://localhost:3000/pedidos/${id}`, {
          method: "DELETE"
        });
        const res = await req.json();

      // msg from system
      this.msg = `Pedido removido com sucesso`

      // clean msg
      setTimeout( () => this.msg = "", 3000 )

        this.getPedidos();
      },
      async updatedPedido(event, id) {
        const option = event.target.value;
        const dataJson = JSON.stringify({ status: option });
        const req = await fetch(`http://localhost:3000/pedidos/${id}`, {
          method: "PATCH",
          headers: { "Content-Type": "application/json" },
          body: dataJson
        });

        const res = await req.json();

     // msg from system
      this.msg = `Pedido Nº ${ res.id } foi atualizado para ${res.status}`

      // clean msg
      setTimeout( () => this.msg = "", 3000 )

      }
    },
    mounted() {
      this.getPedidos()
      this.getListapedido()
    },
    components: {
      Message
    }
  }
</script>
