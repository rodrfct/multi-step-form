<script setup lang="ts">
import Sidebar from './components/Sidebar.vue'
import Form from './components/Form.vue'
</script>

<template>
<div class="wrapper">
  <Sidebar />

  <Form />
</div>
</template>

<style scoped>
.wrapper {
  background-color: var(--Alabaster);
  width: 85%;
  margin: auto;
  padding: 10px;
  border-radius: 15px;
}
</style>
