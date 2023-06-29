<script setup lang="ts">
import { ref } from 'vue';
import Sidebar from './components/Sidebar.vue'
import Form from './components/Form.vue'
import ThankYou from './components/ThankYou.vue'

const step = ref<number>(1)

const isSubmitted = ref<boolean>(false)

const validationPassed = ref<boolean>(false)

const selectStep = (selectedStep: number) => {
  if (!validationPassed.value || isSubmitted.value) {return}

  if (selectedStep >= 1 && selectedStep <= 4) {
    step.value = selectedStep}
  }

</script>

<template>
<div class="wrapper">
  <Sidebar :step="step"
  @selectStep="selectStep" />

  <Form v-if="!isSubmitted" :step="step"
    @stepBack="() => {if (step > 1) {step--}}" 
    @stepForward="() => {if (step < 4 && validationPassed) {step++}}"
    @validated="(val) => {validationPassed = val}"
    @submited="() => {isSubmitted = true}"
  />

  <ThankYou v-else />
</div>
</template>

<style scoped>
.wrapper {
  background-color: var(--Alabaster);
  width: 90%;
  max-width: 800px;
  min-height: 60vh;
  margin: auto;
  padding: 13px;
  border-radius: 15px;

  display: grid;
  grid-template-columns: 33% 1fr;
}

@media (width < 400px) {
  .wrapper {
    grid-template-columns: 1fr;
    grid-template-rows: 40% 1fr;

    padding: 0;
    width: 100%;
    height: 100%;

  }
}

</style>
