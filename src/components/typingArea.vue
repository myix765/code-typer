<template>
    <div>
        <TypingTest
            :currentCodeSnippet="currentCodeSnippet"
        ></TypingTest>
    </div>
</template>

<script>
import TypingTest from './typingTest.vue'

export default {
    props: ['currentCodeSnippet'],
    components: {
        TypingTest,
    },
}
</script>

<style scoped>

</style>