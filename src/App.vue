<template>
    <div id="page-grid">
        <NavBar
            id="navbar"
            :lang-selected="activeLang"
            :length="codeJSONlength"
            :start-new-test="getRandomIndex"
        ></NavBar>
        <LanguagePanel
            id="language-panel"
            class="panel"
            :languages="languages"
            :select-language="changeActiveLang"
        ></LanguagePanel>
        <HistoryPanel
            id="history-panel"
            class="panel"
        ></HistoryPanel>
        <TypingArea
            id="type-panel"
            class="panel"
            @receive-length="getLength"
            :current-block-index="currentBlockIndex"
            :active-lang="activeLang"
        ></TypingArea>
        <StatsPanel
            id="stats-panel"
            class="panel"
        ></StatsPanel>
    </div>
</template>

<script>
import NavBar from './components/navBar.vue'
import LanguagePanel from './components/languagePanel.vue'
import HistoryPanel from './components/historyPanel.vue'
import TypingArea from './components/typingArea.vue'
import StatsPanel from './components/statsPanel.vue'

export default {
    components: {
        NavBar,
        LanguagePanel,
        HistoryPanel,
        TypingArea,
        StatsPanel
    },
    data() {
        return {
            languages: [
                {
                    iconUrl: "https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/python/python-original.svg",
                    langName: "Python"
                },
                {
                    iconUrl: "https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg",
                    langName: "JavaScript"
                }
            ],
            activeLang: "Python",
            codeJSONlength: 0,
            currentBlockIndex: 0,
        }
    },
    methods: {
        getLength(length) {
            this.codeJSONlength = length
            this.getRandomIndex()
        },
        getRandomIndex() {
            this.currentBlockIndex = Math.floor(Math.random() * this.codeJSONlength)
        },
        changeActiveLang(langName) {
            this.activeLang = langName
            this.getRandomIndex()
        }

        // (langName) => activeLang = langName
    },
}
</script>

<style scoped>
@import './style.css';

#page-grid {
    width: 100%;
    height: 100vh;
    display: grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-rows: repeat(7, calc(100vh / 8));
    grid-template-areas: 
        "lang nav nav nav nav"
        "lang type type type stats"
        "lang type type type stats"
        "lang type type type stats"
        "hist type type type stats"
        "hist type type type stats"
        "hist type type type stats"
        "hist type type type stats";
}

#navbar {
    grid-area: nav;
    z-index: 3;
}

#language-panel {
    grid-area: lang;
}

#history-panel {
    grid-area: hist;
    border-top: 1px solid var(--gray-highlight);
}

#type-panel {
    grid-area: type;
    background-color: var(--secondary-background);
    box-shadow: 0 0 0 1px var(--gray-highlight); /* adds border on outside */
}

#stats-panel {
    grid-area: stats;
    box-shadow: 0 -1px 0 var(--gray-highlight); /* adds border on top outside */
}

.panel {
    padding: 4vh 0 0 2vw;
    width: 100%;
    height: 100%;
}
</style>