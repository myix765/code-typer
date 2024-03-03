<template>
    <div>
        <p v-html="formatCode(codeBlocks[currentBlockIndex])"></p>
    </div>
</template>

<script>
import codeJson from '../assets/codeBlocks.json'

export default {
    data() {
        return {
            codeBlocks: [],
            currentBlockIndex: 0,
        }
    },
    created() {
        this.codeBlocks = codeJson.map(block => block.code)
        this.getRandomIndex()
    },
    methods: {
        getRandomIndex() {
            this.currentBlockIndex = Math.floor(Math.random() * this.codeBlocks.length)
        },
        formatCode(code) {
            let lineNum = 1
            // code = `${lineNum} ${code}`
            return code.replace(/(\n|^)/g, function(match) {
                if (match === "\n") {
                    /* case where inserting lineNum at beginning of newline */
                    lineNum++
                    if (lineNum > 9) {
                        return '<br>' + lineNum + '&nbsp;'
                    }
                    return '<br>' + lineNum + '&nbsp;&nbsp;'
                } else {
                    /* case where inserting lineNum at beginning of string */
                    return lineNum + '&nbsp;&nbsp;'
                }
            }).replace(/\t/g, '&nbsp;&nbsp;&nbsp;&nbsp;')
            // return code.replace(/(\n|^)/g, `<br>${lineNum} `).replace(/\t/g, '&nbsp;&nbsp;&nbsp;&nbsp;')
        }
    }
}
</script>

