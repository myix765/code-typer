<template>
    <div>
        <div
            id="nav-div"
        >
            <div class="tab">
                <p>{{ langSelected }}</p>
            </div>
            <button class="start-btn">Start New Test</button>
            <div class="nav-icons">
                <a href="#">
                    
                </a>
            </div>
        </div>
    </div>
</template>

<script>
    import SettingsIcon from '../assets/icons/settings.svg'

    export default {
        props: {
            langSelected: {
                type: String,
                required: true
            }
        },
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
        width: 100%;
        /* background-color: darkgreen; */
        align-items: flex-end;
    }

    .tab {
        box-shadow: 0 1px 0 var(--secondary-background), 0 -1px 0 var(--gray-highlight), 0 0 0 1px var(--gray-highlight);
        background-color: var(--secondary-background);
        padding: 1.8% 2%;
        width: 20%;
        margin-bottom: 1px;
        -moz-border-radius: 0px;
        -webkit-border-radius: 10px 10px 0px 0px;
        border-radius: 10px 10px 0px 0px; 
    }

    .start-btn {
        background-color: var(--primary-background);
        border: 1px solid var(--gray-highlight);
        border-radius: 10px;
        color: var(--white);
        font-family: "Monaco";
        padding: 14px 20px;
        margin: 0 0 1% 1.4%;
        cursor: pointer;
    }

    .start-btn:hover {
        background-color: var(--gray-highlight);
    }

    .icon-link {
        background-color: aliceblue;
        cursor: pointer;
    }
</style>