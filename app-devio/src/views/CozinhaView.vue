<template>
  <div class="about">
    <h1>This is an about page</h1>

  </div>
</template>

<script>
export default {
  name: 'CozinhaView',
  data() {
    return {
      produtos: null,
    }
  },
  methods: {
    async getProdutos() {
            const req = await fetch(`http://localhost:3000/pedidos}`)
            const data = await req.json()

            this.produtos = data
    }
  }
}
</script>
