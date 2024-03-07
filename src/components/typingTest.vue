<template>
    <div id="text">
        <span
            class="snippet-template"
            v-if="currentCodeSnippet"
            v-html="formatCode(currentCodeSnippet)"
        ></span>
        <textarea
            name="text-input"
            id="type-input"
            :cols=snippetCol
            :rows=snippetRow
            @keydown.tab.prevent="insertTab"
            @keydown="checkInputLength"
            v-model="inputText"
            autofocus
        ></textarea>
    </div>
</template>

<script>
export default {
    props: ['currentCodeSnippet'],
    data() {
        return {
            snippetCol: 0,
            snippetRow: 0,
            inputText: "",
        }
    },
    methods: {
        formatCode(snippet) {
            let lineNum = 1
            this.getColAndRow(snippet)
            /* regex to select all \n and beginning of the string */
            return snippet.replace(/(\n|^)/g, function(match) {
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
        getColAndRow(snippet) {
            let maxLength = 0
            let snippetArray = snippet.replace(/\t/g, '    ').split("\n")
            for (let line of snippetArray) {
                if (line.length > maxLength) {
                    maxLength = line.length
                }
            }
            this.snippetRow = snippetArray.length + 1 /* +1 for if user incorrectly types newline */
            this.snippetCol = maxLength + 1 /* +1 for if user incorrectly types newline */
        },
        insertTab(e) {
            const textarea = e.target;
            const start = textarea.selectionStart;
            const end = textarea.selectionEnd;

            // Insert tab character at the cursor position
            this.inputText = this.inputText.substring(0, start) +
                '    ' +
                this.inputText.substring(end);

            // Move cursor position after the inserted tab
            textarea.selectionStart = textarea.selectionEnd = start + 4;

            // Prevent default tab behavior
            e.preventDefault();
        },
        checkInputLength(e) {
            const textarea = e.target;
            const start = textarea.selectionStart;
            const end = textarea.selectionEnd;

            const rows = this.inputText.split('\n');
            const currentRow = this.getRowNumber(start);
            const currentRowLength = rows[currentRow - 1].length;

            if (rows.length == this.snippetRow && e.key == 'Enter') {
                e.preventDefault(); /* prevent typing newline */
            }
            if (currentRow > this.snippetRow || (currentRowLength >= this.snippetCol && start === end)) {
                if (e.keyCode != 8) { /* check if key pressed is not backspace */
                    e.preventDefault(); /* prevent typing more characters */
                }
            }
        },
        getRowNumber(cursorPosition) {
            const textBeforeCursor = this.inputText.substring(0, cursorPosition);
            return textBeforeCursor.split('\n').length;
        }
    }
}
</script>

<style scoped>
    .snippet-template {
        color: var(--gray)
    }

    #text {
        position: relative;
    }

    #type-input {
        position: absolute;
        top: 0;
        left: 0;
        padding-left: 3ch;
    }
</style>