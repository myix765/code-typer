<template>
    <div>
        <div
            id="nav-div"
        >
            <div id="nav-left">
                <div class="tab">
                    <p>{{ langSelected }}</p>
                </div>
                <button
                    class="start-btn"
                    @click.prevent="startNewTest()">Start New Test</button>
            </div>
            <div class="nav-icons">
                <div>
                    <a href="#">
                        <SettingsIcon class="icon-link"></SettingsIcon>
                    </a>
                </div>
                <div>
                    <a href="#">
                        <ProfileIcon class="icon-link"></ProfileIcon>
                    </a>
                </div>
                <div>
                    <a href="#">
                        <PanelIcon class="icon-link"></PanelIcon>
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import SettingsIcon from '../assets/icons/settings.svg'
import ProfileIcon from '../assets/icons/profile.svg'
import PanelIcon from './panelIcon.vue'

export default {
    props: ['langSelected', 'length', 'startNewTest'],
    components: {
        SettingsIcon,
        ProfileIcon,
        PanelIcon
    }
}
</script>

<style scoped>
#nav-div {
    display: flex;
    height: 100%;
    align-items: flex-end;
    justify-content: space-between;
}

#nav-left {
    display: flex;
    align-items: flex-end;
    height: 48%;
    width: 80%;
}

.tab {
    box-shadow: 0 1.5px 0 var(--secondary-background), 0 -1px 0 var(--gray-highlight), 0 0 0 1px var(--gray-highlight); /* extend 1.5px down just in case */
    background-color: var(--secondary-background);
    padding: 1.8% 2.2%;
    height: 100%;
    width: 200px;
    margin-bottom: 1px; /* to hide bottom corner box shadows */
    -webkit-border-radius: 10px 10px 0px 0px;
    border-radius: 10px 10px 0px 0px; 
}

.start-btn {
    background-color: var(--primary-background);
    border: none;
    box-shadow: 0 0 0 1px var(--gray-highlight);
    border-radius: 10px;
    color: inherit;
    font-family: inherit;
    padding: 0 3.2%;
    height: 80%;
    margin-left: 1.5%;
    align-self: flex-start;
    cursor: pointer;
}

.start-btn:hover {
    background-color: var(--gray-highlight);
}

.nav-icons {
    display: flex;
    column-gap: 14px;
    margin: 0.6% 1%;
}

.icon-link {
    cursor: pointer;
    width: 100%;
    height: 100%;
}

a {
    display: flex;
    height: 24px;
}
</style>