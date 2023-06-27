<script setup lang="ts">
import { computed } from 'vue';
import type { selectionsInterface, planPricingInterface, addonsPricingInterface } from './Form.vue';

const props = defineProps<{
    planPricing: planPricingInterface,
    addonsPricing: addonsPricingInterface,
    selections: selectionsInterface
}>()

const total = computed((): number => {
    let base: number = 0

    // Determine the chosen plan (props.planPricing[props.selections.plan] would be much cleaner but doesn't work)
    if (props.selections.plan == "pro") {
        base = props.planPricing.pro[props.selections.periodicity]
    
    } else if (props.selections.plan == "advanced") {
        base = props.planPricing.advanced[props.selections.periodicity]
    
    } else if (props.selections.plan == "arcade") {
        base = props.planPricing.arcade[props.selections.periodicity]
    }

    // Add the price of the selected add-ons
    if (props.selections.addons.onlineService) {
        base += props.addonsPricing.onlineService[props.selections.periodicity]
    }

    if (props.selections.addons.largerStorage) {
        base += props.addonsPricing.largerStorage[props.selections.periodicity]
    }

    if (props.selections.addons.customizableProfile) {
        base += props.addonsPricing.customizableProfile[props.selections.periodicity]
    }

    return base
})

const planPrice = computed(() => {
    if (props.selections.plan == "pro") {
        return `$${props.planPricing.pro[props.selections.periodicity]}/${periodicityAbbreviated.value}`
    
    } else if (props.selections.plan == "advanced") {
        return `$${props.planPricing.advanced[props.selections.periodicity]}/${periodicityAbbreviated.value}`
    
    } else if (props.selections.plan == "arcade") {
        return `$${props.planPricing.arcade[props.selections.periodicity]}/${periodicityAbbreviated.value}`
    }
})

const periodicityAbbreviated = computed(() => props.selections.periodicity == "yearly" ? "yr" : "mo")
</script>

<template>
    <fieldset>
        <legend>Finishing up</legend>
        <p>Double-check everything looks OK before confirming.</p>

        <div class="summary">
            <div class="item plan">
                <div class="selection">
                    <span>{{ selections.plan }} ({{ selections.periodicity }})</span>
                    <p @click="$emit('select-step', 2)">Change</p>
                </div>

                <span class="price">{{ planPrice }}</span>
            </div>

            <div v-if="selections.addons.onlineService" class="item">
                <p>Online service</p>
                <span class="price">{{ `+$${addonsPricing.onlineService[selections.periodicity]}/${periodicityAbbreviated}` }}</span>
            </div>

            <div v-if="selections.addons.largerStorage" class="item">
                <p>Larger storage</p>
                <span class="price">{{ `+$${addonsPricing.largerStorage[selections.periodicity]}/${periodicityAbbreviated}` }}</span>
            </div>

            <div v-if="selections.addons.customizableProfile" class="item">
                <p>Customizable profile</p>
                <span class="price">{{ `+$${addonsPricing.customizableProfile[selections.periodicity]}/${periodicityAbbreviated}` }}</span>
            </div>

        </div>

        <div class="item total">
            <p>Total (per {{ selections.periodicity == "yearly" ? "year" : "month" }})</p>

            <span class="price">{{ `+$${total}/${periodicityAbbreviated}` }}</span>
        </div>
    </fieldset>
</template>

<style scoped>
.summary {
    background-color: var(--Magnolia);
    padding: 15px 0;
    margin-top: 10%;
}

.item {
    display: flex;
    justify-content: space-between;
    align-items: center;

    margin: 2% 6%;
}

.item p {
    margin: 2% 0;
}

.plan {
    border-bottom: 2px solid var(--Light-gray);
}

.plan > span {
    font-weight: 500;
}

.plan > * {
    margin-bottom: 7%;
}

.selection span {
    font-weight: 500;
    text-transform: capitalize;
}

.selection p {
    margin: 5px 0 0 0;
    text-decoration: underline;
    cursor: pointer;

    transition: color .2s ease;
}

.selection p:hover {
    color: var(--Purplish-blue) !important;
}

.total {
    margin-top: 5%;
}

.total span {
    color: var(--Purplish-blue);
    font-weight: 700;
    font-size: 1.1em;
}
</style>