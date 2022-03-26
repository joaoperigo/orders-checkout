<template>
    <div class="input-group mb-3 client-name">
        <input type="text" class="form-control" placeholder="Nome do cliente" aria-label="Recipient's username" aria-describedby="button-addon2">
        <button class="btn btn-outline-secondary" type="button" id="button-addon2">O</button>
    </div>
</template>

<script>
export default {
    name: 'ClientName'
}
</script>

<style scoped>
.client-name {
    padding-top: 100px;
}
</style>