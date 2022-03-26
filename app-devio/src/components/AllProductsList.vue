<template>

<form action="" @submit="sendForm($event)">

    <div class="mb-3">
        <h2>#01 | Nome produto</h2>
        <img src="http://placekitten.com/200/200" alt="">
    </div>

    <div class="mb-3">
        <label for="vegano" class="form-label">Email address</label>
        <select class="form-select" aria-label="Default select example" v-model="restricao">
            <option selected>Selecione restrição alimentar</option>
            <option value="1">Vegano (nada de animal)</option>
            <option value="2">Onívoro (carnes e vegetais)</option>
            <option value="3">Vegetariano (come queijo e ovo)</option>
        </select>
    </div>

    <div class="mb-3">
        <div class="form-check">
            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" v-model="detalhes">
            <label class="form-check-label" for="flexCheckDefault">
                Default checkbox
            </label>
        </div>
    </div>

    <div class="mb-3">
        <label for="observacoes" class="form-label">Email address</label>
        <div class="form-floating">
            <textarea class="form-control" placeholder="Leave a comment here" id="floatingTextarea" v-model="observacoes"></textarea>
            <label for="floatingTextarea">Observações</label>
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
            restricao: null,
            observacoes: null
        }
    },
    methods: {
        sendForm(e) {
            e.preventDefault()

            const restricao = this.restricao
            const observacoes = this.observacoes
            
            console.log(this.restricao)
            console.log(this.detalhes)
            console.log(this.observacoes)
        }
    }
}
</script>