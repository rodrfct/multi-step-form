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

defineEmits(['step-back', 'step-forward', 'select-step'])

const planPricing = {
    arcade: {
        monthly: 9,
        yearly: 90
    },
    advanced: {
        monthly: 12,
        yearly: 120
    },
    pro: {
        monthly: 15,
        yearly: 150
    }
}

const addonsPricing = {
    onlineService: {
        monthly: 1,
        yearly: 10
    },
    largerStorage: {
        monthly: 2,
        yearly: 20
    },
    customizableProfile: {
        monthly: 2,
        yearly: 20
    }
}

const yearlyPlan = ref<boolean>(false)

const form = ref<HTMLFormElement | null>(null)

function getFormValue() {
    return {
        // @ts-expect-error
        name: form.value?.elements.name.value,
        // @ts-expect-error
        email: form.value?.elements.email.value,
        // @ts-expect-error
        phone: form.value?.elements.phone.value,
        // @ts-expect-error
        plan: form.value?.elements.plan.value,
        // @ts-expect-error
        periodicity: form.value?.elements.periodicity.checked ? "yearly" : "monthly",
        // @ts-expect-error
        onlineService: form.value?.elements.online.checked,
        // @ts-expect-error
        largerStorage: form.value?.elements.storage.checked,
        // @ts-expect-error
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

        <Step2 v-show="props.step == 2" :planPricing="planPricing"
        :yearlyPlan="yearlyPlan"
        @periodicityChange="(val: boolean) => {yearlyPlan = val}" />

        <Step3 v-show="props.step == 3" :addonsPricing="addonsPricing" :yearlyPlan="yearlyPlan" />

        <Step4 v-show="props.step == 4"
        :selections="getFormValue()"
        :planPricing="planPricing"
        :addonsPricing="addonsPricing"
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