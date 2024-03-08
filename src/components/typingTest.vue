<template>
    <div id="typing-test">
        <div id="text">
            <span
                class="snippet-template"
                v-if="currentCodeSnippet"
                v-for="(char, index) in formatCode(currentCodeSnippet)"
                :key="index"
                :class="{ 'wrong-letter': checkAccuracy(char, index) }"
                v-html=char
            ></span>
            <textarea
                name="text-input"
                id="type-input"
                v-model="inputText"
                @keyup="getCaretPosition"
                @keydown="bindInputLength"
                @keydown.tab.prevent="insertTab"
                autofocus
            ></textarea>
        </div>
    </div>
</template>

<script>
export default {
    props: ['currentCodeSnippet', 'snippetCols', 'snippetRows'],
    data() {
        return {
            snippetArr: [],
            inputText: "",
            caretPosition: 0,
        }
    },
    methods: {
        formatCode(snippet) {
            /* regex to select all \n and beginning of the string */
            let charArr = snippet.split('')

            this.snippetArr = charArr.map(char => {
                if (char === '\n') {
                    return '<br>'
                } else if (char === '\t') {
                    return '&nbsp;&nbsp;&nbsp;&nbsp;'
                } else {
                    return char
                }
            })

            return this.snippetArr
        },
        checkAccuracy(char, index) { // isn't working correctly with newlines and tabs
            return (this.inputText[index] !== undefined && this.inputText[index] !== char)
        },
        insertTab(e) { // currently pressing tab in middle of characters sends cursor to end of textarea
            const textarea = e.target
            const start = textarea.selectionStart
            const end = textarea.selectionEnd

            // Insert tab character at the cursor position
            this.inputText = this.inputText.substring(0, start) +
                '    ' + this.inputText.substring(end)

            // Move cursor position after the inserted tab
            // textarea.selectionStart = textarea.selectionEnd = start + 4;
            // console.log("add " + (start + 4))
            // textarea.setSelectionRange(start + 4, start + 4)

            // Prevent default tab behavior
            // e.preventDefault();
            // textarea.selectionStart = textarea.selectionEnd = start + 4;
        },
        // getCaretPosition(e) {
        //     const textarea = e.target
        //     let caretPosition = textarea.selectionStart;
        //     this.caretPosition = caretPosition
        // },
        bindInputLength(e) { // allow them to press ctrl/cmd?
            const textarea = e.target;
            const start = textarea.selectionStart;
            const end = textarea.selectionEnd;

            const rows = this.inputText.split('\n');
            const currentRow = this.getRowNumber(start);
            const currentRowLength = rows[currentRow - 1].length;

            if (rows.length == this.snippetRows && e.key == 'Enter') {
                e.preventDefault(); /* prevent typing newline */
            }
            if (currentRow > this.snippetRows || (currentRowLength >= this.snippetCols && start === end)) {
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
#typing-test {
    width: 100%;
}

.snippet-template {
    color: var(--gray)
}

#text {
    position: relative;
    height: 100%;
    width: 100%;
}

#type-input {
    position: absolute;
    top: 0;
    left: 0;
}

.wrong-letter {
    background-color: var(--wrong-highlight);
    color: var(--wrong-highlight);
}
</style>