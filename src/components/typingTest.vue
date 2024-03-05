<template>
    <p
        v-if="currentCodeSnippet"
        v-html="formatCode(currentCodeSnippet)"
    ></p>
</template>

<script>
export default {
    props: ['currentCodeSnippet'],
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
    }
}
</script>

<style>

</style>