<script setup lang="ts">
import { ref } from 'vue';
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

const form = ref<HTMLFormElement | null>(null)

function getFormValue() {
        return {
        name: form.value?.elements.name.value,
        email: form.value?.elements.email.value,
        phone: form.value?.elements.phone.value,
        plan: form.value?.elements.plan.value,
        periodicity: form.value?.elements.periodicity.checked,
        onlineService: form.value?.elements.online.checked,
        largerStorage: form.value?.elements.storage.checked,
        customizableProfile: form.value?.elements.customizable.checked
    }
}

function submitForm() {
    console.log(getFormValue())
}

</script>

<template>
    <form ref="form" id="form">
        <Step1 v-show="props.step == 1" />
        <Step2 v-show="props.step == 2" />
        <Step3 v-show="props.step == 3" />
        <Step4 v-show="props.step == 4"
        @selectStep="(selectedStep) => {$emit('select-step', selectedStep)}" />
    
        <div class="step-switcher">
            <button v-show="props.step > 1" @click="$emit('step-back')" type="button" id="back-btn">Go Back</button>
            <button v-show="props.step < 4" @click="$emit('step-forward')" type="button" id="forward-btn">Next Step</button>
            <button v-show="props.step == 4" type="button" id="confirm-btn"
            @click="submitForm">Confirm</button>
        </div>
    </form>
</template>

<style>
#form {
    position: relative;
    margin: 0 13%;
    color: var(--Marine-blue);
}

/*Buttons */
.step-switcher {
    width: 100%;
    display: grid;
    grid-auto-flow: column;
    
    position: absolute;
    bottom: 5%;
}

.step-switcher button {
    border: none;
    border-radius: 6px;
    padding: .7em 1.5em;
}

#forward-btn {
    background-color: var(--Marine-blue);
    color: var(--White);
    font-weight: 700;

    justify-self: end;
}

#back-btn {
    border: none;
    background-color: inherit;
    color: var(--Cool-gray);

    justify-self: start;
}

#confirm-btn {
    background-color: var(--Purplish-blue);
    color: var(--White);
    font-weight: 700;
    justify-self: end;
}

/*Actual form */
#form fieldset {
    border: none;
    padding: 0;
    margin: 8% 0 8% 0;
}

#form legend {
    font-size: 1.75em;
    font-weight: 700;
}

#form p {
    color: var(--Cool-gray);
}

</style>