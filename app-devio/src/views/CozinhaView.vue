<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
      <Message :msg="msg" v-show="msg" />
          <table class="mx-auto table-responsive">
            <thead>
              <tr>
                <th scope="col">Id</th>
                <th scope="col">Nome</th>
                <th scope="col">Qtd</th>
                <th scope="col">Produto</th>
                <th scope="col">Status</th>
                <th scope="col">Cancelar</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="pedido in pedidos" :key="pedido.id">
                <th scope="row">#{{pedido.id}}</th>
                <td>{{pedido.nome}}</td>
                <td>
                  <p class="qtd-produto" v-for="lista in pedido.pedido" :key="lista.id">
                    <b>{{lista.qtd}}</b> 
                  </p>
                </td>
                <td>
                  <p class="qtd-produto" v-for="lista in pedido.pedido" :key="lista.id">
                    <b> {{lista.tituloProduto}} </b> 
                  </p>
                </td>
                <td>
                  <div>
                    <select name="status" class="status" @change="updatedPedido($event, pedido.id)">
                      <option value="">Selecione </option>
                      <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="pedido.status == s.tipo">{{ s.tipo }}</option>
                    </select>
                  </div>
                </td>
                <td>
                  <button class="delete-btn" @click="deletePedido(pedido.id)">Cancelar</button>
                </td>
              </tr>
              
            </tbody>
          </table>
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
        msg: null,
        produtos: null,
        pedidoNome: null
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
      // resolver pega titulo produto pelo id do pedido[]
      // async getProduto() {
      //   const req = await fetch("http://localhost:3000/produtos")
      //   const data = await req.json();
      //   this.produtos = data;
      // },
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
      // this.getProduto()
    },
    components: {
      Message
    }
  }
</script>



<style lang="scss" scoped>
  td, th {
    padding: 15px 25px;
    border-bottom: solid 1px var(--dark);
  }
  tr:nth-child(even), thead tr {
    background-color: var(--neutral);
  }
</style>