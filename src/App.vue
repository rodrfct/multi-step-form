<script setup lang="ts">
import { ref } from 'vue';
import Sidebar from './components/Sidebar.vue'
import Form from './components/Form.vue'
import ThankYou from './components/ThankYou.vue'

const step = ref<number>(1)

const isSubmitted = ref<boolean>(false)

</script>

<template>
<div class="wrapper">
  <Sidebar :step="step"
  @selectStep="(selectedStep) => {if (selectedStep >= 1 && selectedStep <= 4) {step = selectedStep}}" />

  <Form v-if="!isSubmitted" :step="step"
  @stepBack="() => {if (step > 1) {step--}}" 
  @stepForward="() => {if (step < 4) {step++}}"
  @selectStep="(selectedStep) => {if (selectedStep >= 1 && selectedStep <= 4) {step = selectedStep}}"
  @submit.prevent="() => {isSubmitted = true}" />

  <ThankYou v-else />
</div>
</template>

<style scoped>
.wrapper {
  background-color: var(--Alabaster);
  width: 85%;
  height: 550px;
  margin: auto;
  padding: 13px;
  border-radius: 15px;

  display: grid;
  grid-template-columns: 33% 1fr;
}
</style>
