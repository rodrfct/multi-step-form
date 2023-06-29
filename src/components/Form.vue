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

const emit = defineEmits(['step-back', 'step-forward', 'select-step', 'submited', 'validated'])

export interface planPricingInterface {
    arcade: {
        monthly: number,
        yearly: number
    },
    advanced: {
        monthly: number,
        yearly: number
    },
    pro: {
        monthly: number,
        yearly: number
    }
}

export interface addonsPricingInterface {
    onlineService: {
        monthly: number,
        yearly: number
    },
    largerStorage: {
        monthly: number,
        yearly: number
    },
    customizableProfile: {
        monthly: number,
        yearly: number
    }
}

export interface addonsInterface {
    onlineService: boolean,
    largerStorage: boolean,
    customizableProfile: boolean
}

export interface personalInfoInterface {
    name: string,
    mail: string,
    phone: string
}

export type Plan = "pro" | "advanced" | "arcade"
export type Periodicity = "yearly" | "monthly"

export interface selectionsInterface {
    personalInfo: personalInfoInterface, 
    plan: Plan,
    periodicity: Periodicity,
    addons: addonsInterface
}

const planPricing: planPricingInterface = {
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

const addonsPricing: addonsPricingInterface = {
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

const selections = ref<selectionsInterface>({
    personalInfo: {
        name: '',
        mail: '',
        phone: ''
    },
    plan: 'arcade',
    periodicity: 'monthly',
    addons: {
        onlineService: false,
        largerStorage: false,
        customizableProfile: false
    }
})

function submitForm() {
    console.log(selections.value)
    emit('submited')
}

</script>

<template>
    <form id="form">
        <Step1 v-if="props.step == 1"
            :selectionsStep1="selections?.personalInfo"
            @nameChange="(val: string) => {selections.personalInfo.name = val }"
            @mailChange="(val: string) => {selections.personalInfo.mail = val }"
            @phoneChange="(val: string) => {selections.personalInfo.phone = val }"
            @validated="(val: boolean) => {$emit('validated', val)}"
        />

        <Step2 v-else-if="props.step == 2" :planPricing="planPricing"
            :selectedPlan="selections.plan"
            :yearlyPlan="selections.periodicity"
            @planChange="(val: Plan) => {selections.plan = val}"
            @periodicityChange="(val: boolean) => {val ? selections.periodicity = 'yearly' : selections.periodicity = 'monthly'}"
        />

        <Step3 v-else-if="props.step == 3"
            :addonsPricing="addonsPricing"
            :yearlyPlan="selections.periodicity"
            :seletedAddons="selections.addons"
            @onlineServiceChange="(val: boolean) => {selections.addons.onlineService = val}"
            @largerStorageChange="(val: boolean) => {selections.addons.largerStorage = val}"
            @customizableProfileChange="(val: boolean) => {selections.addons.customizableProfile = val}"
        />

        <Step4 v-else-if="props.step == 4"
            :selections="selections"
            :planPricing="planPricing"
            :addonsPricing="addonsPricing"
            @selectStep="(selectedStep) => {$emit('select-step', selectedStep)}" 
        />
    
        <div class="step-switcher">
            <button v-show="props.step > 1" @click="$emit('step-back')" type="button" id="back-btn">Go Back</button>
            <button v-show="props.step < 4" @click="$emit('step-forward')" type="button" id="forward-btn">Next Step</button>
            <button v-show="props.step == 4" type="button" id="confirm-btn" @click="submitForm">Confirm</button>
        </div>
    </form>
</template>

<style>
#form {
    position: relative;
    margin: 0 13%;
    padding-bottom: 20%;
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
    font-weight: 700;
}

.step-switcher button:hover {
    cursor: pointer;
}

#forward-btn {
    background-color: var(--Marine-blue);
    color: var(--White);
    transition: filter .3s ease;

    justify-self: end;
}

#forward-btn:hover, #confirm-btn:hover {
    filter: brightness(150%);
}

#back-btn {
    border: none;
    background-color: inherit;
    color: var(--Cool-gray);

    justify-self: start;
}

#back-btn:hover {
    color: var(--Marine-blue);
}

#confirm-btn {
    background-color: var(--Purplish-blue);
    color: var(--White);
    font-weight: 700;
    justify-self: end;

    transition: filter .5s ease;
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

@media (width < 400px) {
    #form {
        position: relative;
        padding: 0;
        margin: 0;
    }

    #form fieldset {
        position: absolute;
        top: -75px;

        margin: 0 5%;
        padding: 40px 20px 20px 20px;

        background-color: var(--Alabaster);
        border-radius: 15px;

        box-shadow: -1px 1px 4px #999;
    }

    #form fieldset legend {
        position: relative;
        top: 30px;
    }

    .step-switcher {
        position: fixed;
        bottom: 0;

        background-color: var(--Alabaster);
        padding: 10px;
    }
}

</style>