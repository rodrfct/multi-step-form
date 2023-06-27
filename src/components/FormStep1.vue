<script setup lang="ts">
import { computed } from 'vue'
import type { personalInfoInterface } from './Form.vue'

const props = defineProps<{
    selectionsStep1: personalInfoInterface | undefined
}>()

const emit = defineEmits(['name-change', 'mail-change', 'phone-change'])

const name = computed({
    get() {
        return props.selectionsStep1?.name
    },
    set(newValue) {
        emit('name-change', newValue)
    }
})

const mail = computed({
    get() {
        return props.selectionsStep1?.mail
    },
    set(newValue) {
        emit('mail-change', newValue)
    }
})
const phone = computed({
    get() {
        return props.selectionsStep1?.phone
    },
    set(newValue) {
        emit('phone-change', newValue)
    }
})
</script>

<template>
    <fieldset>
        <legend>Personal info</legend>
        <p>Please provide your name, email address, and phone number.</p>

        <label for="name">Name</label>
        <input v-model.lazy="name" class="form-control" type="text" name="name" id="name" placeholder="e.g. Stephen King">

        <label for="email">Email Address</label>
        <input v-model.lazy="mail" class="form-control" type="email" name="email" id="email" placeholder="e.g. stephenking@lorem.com">

        <label for="phone">Phone Number</label>
        <input v-model.lazy="phone" class="form-control" type="tel" name="phone" id="phone" placeholder="e.g. +1 234 567 890">
    </fieldset>
</template>

<style scoped>
.form-control {
    display: block;
    width: 100%;

    padding: .7em;
    margin: 2% 0 5% 0;

    border: 1px solid var(--Light-gray);
    border-radius: 7px;
}
</style>