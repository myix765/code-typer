<template>
    <div>
        <div
            id="line-nums"
            v-for="num in Array.from({ length: snippetRows - 1}, (_, i) => i + 1)"
            v-html=num
        ></div>
    </div>
</template>

<script>
    export default {
        props: ['snippetRows'],
    }
</script>

<style scoped>
</style>