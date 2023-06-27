<script setup lang="ts">
import { computed } from 'vue';
import type { addonsPricingInterface, addonsInterface, Periodicity } from './Form.vue';

const props = defineProps<{
    addonsPricing: addonsPricingInterface,
    seletedAddons: addonsInterface,
    yearlyPlan: Periodicity
}>()

const emit = defineEmits(['onlineService-change', 'largerStorage-change', 'customizableProfile-change'])

const onlineService = computed({
    get() {
        return props.seletedAddons?.onlineService
    },
    set(newValue) {
        emit('onlineService-change', newValue)
    }
})

const largerStorage = computed({
    get() {
        return props.seletedAddons?.largerStorage
    },
    set(newValue) {
        emit('largerStorage-change', newValue)
    }
})
const customizableProfile = computed({
    get() {
        return props.seletedAddons?.customizableProfile
    },
    set(newValue) {
        emit('customizableProfile-change', newValue)
    }
})
</script>

<template>
    <fieldset>
        <legend>Pick add-ons</legend>
        <p>Add-ons help enhance your gaming experience</p>

        <div class="addons-selector">

            <div class="addon">
                <div class="checkbox">
                    <input type="checkbox" v-model="onlineService" name="online-service" id="online">
                </div>
                
                <div class="text">
                    <label for="online">Online service</label>
                    <p>Access to multiplayer games</p>
                </div>

                <span>{{ yearlyPlan == "yearly" ? `+$${addonsPricing.onlineService.yearly}/yr` : `+$${addonsPricing.onlineService.monthly}/mo` }}</span>
            </div>

            <div class="addon">
                <div class="checkbox">
                    <input type="checkbox" v-model="largerStorage" name="larger-storage" id="storage">
                </div>
                
                <div class="text">
                    <label for="storage">Larger storage</label>
                    <p>Extra 1TB of cloud save</p>
                </div>

                <span>{{ yearlyPlan == "yearly" ? `+$${addonsPricing.largerStorage.yearly}/yr` : `+$${addonsPricing.largerStorage.monthly}/mo` }}</span>
            </div>

            <div class="addon">
                <div class="checkbox">
                    <input type="checkbox" v-model="customizableProfile" name="customizable-profile" id="customizable">
                </div>

                <div class="text">
                    <label for="customizable">Customizable profile</label>
                    <p>Custom theme on your profile</p>
                </div>

                <span>{{ yearlyPlan == "yearly" ? `+$${addonsPricing.customizableProfile.yearly}/yr` : `+$${addonsPricing.customizableProfile.monthly}/mo` }}</span>
            </div>

        </div>
    </fieldset>
</template>

<style scoped>
.addons-selector {
    margin-top: 10%;
}

.addon {
    border: 1px solid var(--Light-gray);
    border-radius: 8px;

    padding: 5%;
    margin: 5% 0;

    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: 5%;
    align-items: center;

    position: relative;
}

.addon label {
    font-weight: 500;
}

.addon p {
    margin: 5px 0 0 0;
}

.addon span {
    color: var(--Purplish-blue);
}

.addon:has(input:checked) {
    border-color: var(--Purplish-blue);
    background-color: var(--Almost-transparent-purplish-blue);
}

.checkbox {
    width: 15px;
    height: 15px;

    border: 1px solid var(--Light-gray);
    border-radius: 3px;
}

.checkbox:has(input:checked) {
    background-color: var(--Purplish-blue);
    background-image: url('../assets/icons/icon-checkmark.svg');
    background-repeat: no-repeat;
    background-size: 70%;
    background-position: 3px 3px;
}

.checkbox input {
    appearance: none;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;

    margin: 0;
}
</style>