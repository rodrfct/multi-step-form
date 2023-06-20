<script setup lang="ts">
import { ref } from 'vue';
import Sidebar from './components/Sidebar.vue'
import Form from './components/Form.vue'

const step =ref<number>(1)

</script>

<template>
<div class="wrapper">
  <Sidebar :step="step"
  @selectStep="(selectedStep) => {if (selectedStep >= 1 && selectedStep <= 4) {step = selectedStep}}" />

  <Form :step="step"
  @stepBack="() => {if (step > 1) {step--}}" 
  @stepForward="() => {if (step < 4) {step++}}" />
</div>
</template>

<style scoped>
.wrapper {
  background-color: var(--Alabaster);
  width: 85%;
  margin: auto;
  padding: 10px;
  border-radius: 15px;

  display: grid;
  grid-template-columns: 30% 1fr;
}
</style>
