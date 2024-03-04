<template>
    <div>
        <p
            v-if="codeBlocks[currentBlockIndex]"
            v-html="formatCode(codeBlocks[currentBlockIndex])"
        ></p>
    </div>
</template>

<script>
import codeJson from '../assets/codeBlocks.json'

export default {
    props: ['currentBlockIndex', 'activeLang'],
    emits: ['receive-length'],
    data() {
        return {
            codeBlocks: [],
        }
    },
    created() {
        // this.codeBlocks = codeJson.map(block => block.code)
        this.getCodeOfLang()
        const length = this.codeBlocks.length
        this.$emit('receive-length', length)
    },
    watch: {
        activeLang(newLang, oldLang) {
            this.getCodeOfLang()
        }
    },
    methods: {
        formatCode(code) {
            let lineNum = 1
            /* regex to select all \n and beginning of the string */
            return code.replace(/(\n|^)/g, function(match) {
                if (match === "\n") {
                    /* case where inserting lineNum at beginning of newline */
                    lineNum++
                    if (lineNum > 9) {
                        return '<br>' + lineNum + ' '
                    }
                    return '<br>' + lineNum + '&nbsp;&nbsp;'
                } else {
                    /* case where inserting lineNum at beginning of string */
                    return lineNum + '&nbsp;&nbsp;'
                }
            }).replace(/\t/g, '&nbsp;&nbsp;&nbsp;&nbsp;')
        },
        getCodeOfLang() {
            this.codeBlocks = codeJson
                .filter(block => block.language === this.activeLang)
                .map(block => block.code)
        }
    }
}
</script>

