<template>
    <div>
        <div id="typing-area">
            <LineNums
                id="line-nums"
                :snippetRows="snippetRows"
            >
            </LineNums>
            <TypingTest
                :currentCodeSnippet="currentCodeSnippet"
                :snippetCols="snippetCols"
                :snippetRows="snippetRows"
            ></TypingTest>
        </div>
    </div>
</template>

<script>
import TypingTest from './typingTest.vue'
import LineNums from './lineNums.vue'

export default {
    props: ['currentCodeSnippet'],
    components: {
        TypingTest,
        LineNums,
    },
    data() {
        return {
            snippetCols: 0,
            snippetRows: 0,
        }
    },
    created() {
        this.getColAndRow(this.currentCodeSnippet)
    },
    methods: {
        getColAndRow(snippet) {
            let maxLength = 0
            let snippetArray = snippet.replace(/\t/g, '    ').split("\n")
            for (let line of snippetArray) {
                if (line.length > maxLength) {
                    maxLength = line.length
                }
            }
            this.snippetRows = snippetArray.length + 1 /* +1 for if user incorrectly types newline */
            this.snippetCols = maxLength + 1 /* +1 for if user incorrectly types newline */
        },
    }
}
</script>

<style scoped>
    #typing-area {
        display: flex;
        height: 100%;
        width: 100%;
    }

    #line-nums {
        font-family: inherit;
        color: var(--gray);
        width: 3ch;
        height: 100%;
    }
</style>