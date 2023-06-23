<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps({
    planPricing: {
        type: Object,
        required: true
    },
    yearlyPlan: Boolean
})

const emit = defineEmits(['periodicity-change'])

const yearly = computed({
    get() {
        return props.yearlyPlan
    },
    set(newValue) {
        emit('periodicity-change', newValue)
    }
})
</script>

<template>
    <fieldset>
        <legend>Select you plan</legend>
        <p>You have the option of monthly or yearly billing</p>

        <div class="plan-selector">
            <div class="plan arcade">
                <img src="../assets/icons/icon-arcade.svg" alt="">
                <label for="arcade">Arcade</label>
                <p class="pricing">{{ yearlyPlan ? `$${planPricing.arcade.yearly}/yr` : `$${planPricing.arcade.monthly}/mo`}}</p>
                <p v-if="yearlyPlan" class="discount">2 months free</p>

                <input type="radio" name="plan" value="arcade" id="arcade" checked>
            </div>

            <div class="plan advanced">
                <img src="../assets/icons/icon-advanced.svg" alt="">
                <label for="advanced">Advanced</label>
                <p class="pricing">{{ yearlyPlan ? `$${planPricing.advanced.yearly}/yr` : `$${planPricing.advanced.monthly}/mo`}}</p>
                <p v-if="yearlyPlan" class="discount">2 months free</p>

                <input type="radio" name="plan" value="advanced" id="advanced">
            </div>

            <div class="plan pro">
                <img src="../assets/icons/icon-pro.svg" alt="">
                <label for="pro">Pro</label>
                <p class="pricing">{{ yearlyPlan ? `$${planPricing.pro.yearly}/yr` : `$${planPricing.pro.monthly}/mo`}}</p>
                <p v-if="yearlyPlan" class="discount">2 months free</p>

                <input type="radio" name="plan" value="pro" id="pro">
            </div>

            <div class="periodicity">
                <span>Monthly</span>

                <label class="switch">
                    <input v-model="yearly" type="checkbox" name="periodicity">
                    <span class="slider"></span>
                </label>
                
                <span>Yearly</span>
            </div>
        </div>
    </fieldset>
</template>

<style scoped>
.plan-selector {
    margin-top: 10%;

    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 13% 15px;
}

.plan {
    padding: 13px;

    border: 1px solid var(--Light-gray);
    border-radius: 10px;
    position: relative;
}

.plan img {
    display: block;
    margin-bottom: 25%;
}

.plan label {
    font-weight: 500;
}

.plan p {
    margin: 3px 0 0 0;
    font-size: .9em;
}

.plan .discount {
    color: var(--Marine-blue) !important;
    font-size: .75em;
} 

.plan input {
    appearance: none;
    position: absolute;
    margin: 0;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
}

.plan:has(input:checked) {
    border-color: var(--Purplish-blue);
    background-color: var(--Almost-transparent-purplish-blue);
}

/*Switch*/
.periodicity {
    grid-column: 1/-1;
    background-color: var(--Magnolia);
    padding: 10px;
    text-align: center;

    font-weight: 500;
}

.periodicity span {
    vertical-align: middle;
}

.switch {
    position: relative;
    display: inline-block;
    width: 45px;
    height: 25px;

    margin: 0 5%;
}

.switch input {
    appearance: none;
}

.slider {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  cursor: pointer;
  background-color: #ccc;
  
  transition: .4s;
  
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 69%;
  width: 39%;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: .4s;

  border-radius: 50%;
}

input:checked + .slider {
  background-color: var(--Marine-blue);
}

input:checked + .slider:before {
  transform: translateX(97%);
}
</style>