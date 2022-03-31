<template>
    <button>Pagar: R$50,00</button>
</template>

<script>
export default {
    name: 'ButtonPay',
}
</script>
<style lang="scss" scoped>
    button {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateY(-50%) translateX(-50%);
        border-radius: 10px;
        background-color: var(--dark);
        border: solid 1px var(--dark);
        padding: 10px 15px;
        color: var(--light);
    }
</style>