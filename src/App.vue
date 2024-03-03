<template>
    <div id="page-grid">
        <NavBar
            id="navbar"
            :lang-selected="activeLang"
        ></NavBar>
        <LanguagePanel
            id="language-panel"
            class="panel"
            :languages="languages"
            :select-language="(langName) => activeLang = langName"
        ></LanguagePanel>
        <HistoryPanel
            id="history-panel"
            class="panel"
        ></HistoryPanel>
        <TypingArea id="type-panel"></TypingArea>
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
                activeLang: "Python"
            }
        },
        methods: {

        }
    }
</script>

<style>
    @import './style.css';
    #page-grid {
        width: 100%;
        height: 100vh;
        display: grid;
        grid-template-columns: repeat(20%);
        grid-template-rows: repeat(calc(100vh / 8));
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
        padding: 4vh 0 0 10%;
    }
</style>