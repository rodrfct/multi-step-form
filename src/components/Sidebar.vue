<script setup lang="ts">
import { computed } from 'vue';
import bgDesktop from '../assets/backgrounds/bg-sidebar-desktop.svg'
import bgMobile from '../assets/backgrounds/bg-sidebar-mobile.svg'

const props = defineProps({
    step: {
        type: Number,
        required: true
    }
})

const bgImage = computed(() => {
    if (window.innerWidth > 420) {
        return bgDesktop
    } else {
        return bgMobile
    }
})

</script>

<template>
    <div class="sidebar" :style="{backgroundImage: `url(${bgImage})`}">
        <ol>
            <li :class="{ active: props.step == 1}">
                <div class="number"><p>1</p></div>

                <div class="text">
                    <span>Step 1</span>
                    <p>Your info</p>
                </div>
            </li>
            <li :class="{ active: props.step == 2}">
                <div class="number"><p>2</p></div>

                <div class="text">
                    <span>Step 2</span>
                    <p>Select plan</p>
                </div>
            </li>
            <li :class="{ active: props.step == 3}">
                <div class="number"><p>3</p></div>

                <div class="text">
                    <span>Step 3</span>
                    <p>Add-ons</p>
                </div>
            </li>
            <li :class="{ active: props.step == 4}">
                <div class="number"><p>4</p></div>

                <div class="text">
                    <span>Step 4</span>
                    <p>Summary</p>
                </div>
            </li>
        </ol>
    </div>
</template>

<style scoped>
.sidebar {
    width: 30%;
    padding: 10px 0;

    background-repeat: no-repeat;
    background-size: cover;
}

.sidebar ol {
    list-style: none;
    margin: auto;

    color: var(--White);
}

/* .sidebar li {
    display: flex;
    justify-content: space-between;
} */

.sidebar li {
    margin: 10% 0;

    display: grid;
    grid-template-rows: 1fr;
    grid-template-columns: auto 1fr;
    column-gap: 9%;
}

.text {
    display: inline;
}

.text p {
    text-transform: uppercase;
    font-weight: 500;
    margin: 0;
}

.text span {
    color: var(--Pastel-blue);
    text-transform: uppercase;
    font-size: .8em;
}

.number {
    display: inline-block;
    align-self: center;
    text-align: center;

    --size: 28px;
    width: var(--size);
    height: var(--size);
    
    border: 1px solid var(--White);
    border-radius: 15px;
}

.number p {
    display: inline;
    vertical-align: middle;
    font-weight: 500;
}

.active .number {
    background-color: var(--Pastel-blue);
    color: var(--Marine-blue);
    border-color: var(--Pastel-blue);
}
</style>