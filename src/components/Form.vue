<script setup lang="ts">
import Step1 from './FormStep1.vue'
import Step2 from './FormStep2.vue'
import Step3 from './FormStep3.vue'
import Step4 from './FormStep4.vue'

const props = defineProps({
    step: {
        type: Number,
        required: true
    }
})

</script>

<template>
    <form>
        <Step1 v-if="props.step == 1" />
        <Step2 v-else-if="props.step == 2" />
        <Step3 v-else-if="props.step == 3" />
        <Step4 v-else-if="props.step == 4" />
    
        <div class="step-switcher">
            <button v-show="props.step > 1" @click="$emit('step-back')" type="button" id="back-btn">Go Back</button>
            <button v-show="props.step <= 4" @click="$emit('step-forward')" type="button" id="forward-btn">Next Step</button>
        </div>
    </form>
</template>

<style scoped>
form {
    padding: 0 10%;
}

.step-switcher {
    width: 100%;
    position: relative;
}

#forward-btn {
    border: none;
    border-radius: 6px;

    padding: .7em 1.3em;
    background-color: var(--Marine-blue);
    color: var(--White);
    font-weight: 700;

    position: absolute;
    right: 0;
}

#back-btn {
    border: none;
    background-color: inherit;
    color: var(--Cool-gray);

    position: absolute;
    left: 0;
}
</style>