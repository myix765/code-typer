<template>
    <div>
        <h3>LANGUAGES</h3>
        <div id="lang-list" >
            <a
                class="lang-option"
                v-for="(language) in languages"
                @click.prevent="selectLanguage(language.langName)"
            >
                <img
                    :src="language.iconUrl"
                    class="lang-icon"
                />
                <p>{{ language.langName }}</p>
            </a>
        </div>
    </div>
</template>

<script>
export default {
    props: ['languages', 'selectLanguage']
}
</script>

<style scoped>
#lang-list {
    display: flex;
    flex-direction: column;
    gap: 1vh;
}

.lang-option {
    display: flex;
    align-items: center;
    gap: 3%;
    cursor: pointer;
    padding: 2% 4%;
}

.lang-option:hover {
    background-color: rgb(116, 145, 155);
}

.lang-icon {
    width: 24px;
}
</style>