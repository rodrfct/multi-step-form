<script setup lang="ts">
import { reactive, watch } from 'vue'
import { useAsyncValidator } from '@vueuse/integrations/useAsyncValidator' 
import type { personalInfoInterface } from './Form.vue'
import type { Rules } from 'async-validator';

const props = defineProps<{
    selectionsStep1: personalInfoInterface
}>()

const emit = defineEmits(['name-change', 'mail-change', 'phone-change', 'validated'])

const form = reactive({
        name: props.selectionsStep1.name,
        mail: props.selectionsStep1.mail,
        phone: props.selectionsStep1.phone
    })

const rules: Rules = {
  name: {
    type: 'string',
    min: 5,
    max: 20,
    required: true,
  },
  mail: [
    {
      type: 'email',
      required: true,
    },
  ],
  phone: {
    type: 'pattern',
    pattern: /^(?:\+\d{1,3}\s?)?\(?\d{1,4}\)?[-.\s]?\d{1,4}[-.\s]?\d{1,9}$/,
    required: true
  }
}

watch(
    () => form.name,
    (newVal) => {
        emit('name-change', newVal)
    }
)

watch(
    () => form.mail,
    (newVal) => {
        emit('mail-change', newVal)
    }
)

watch(
    () => form.phone,
    (newVal) => {
        emit('phone-change', newVal)
    }
)

const { pass, isFinished, errorFields } = useAsyncValidator(form, rules)

watch(
    () => pass.value,
    (newVal) => {
        emit('validated', newVal)
    }
)

</script>

<template>
    <fieldset>
        <legend>Personal info</legend>
        <p>Please provide your name, email address, and phone number.</p>

        <label for="name">
            Name
            
            <span v-if="errorFields?.name?.length" class="error-msg">{{ errorFields.name[0].message }}</span>
        </label>
        <input v-model.lazy="form.name" class="form-control" :class="{errorInput: errorFields?.name?.length}" type="text" name="name" id="name" placeholder="e.g. Stephen King">

        <label for="email">
            Email Address

            <span v-if="errorFields?.mail?.length" class="error-msg">{{ errorFields.mail[0].message }}</span>
        </label>
        <input v-model.lazy="form.mail" class="form-control" :class="{errorInput: errorFields?.mail?.length}" type="email" name="email" id="email" placeholder="e.g. stephenking@lorem.com">

        <label for="phone">
            Phone Number

            <span v-if="errorFields?.phone?.length" class="error-msg">{{ errorFields.phone[0].fieldValue ? "Phone number is invalid": errorFields.phone[0].message }}</span>
        </label>
        <input v-model.lazy="form.phone" class="form-control" :class="{errorInput: errorFields?.phone?.length}" type="tel" name="phone" id="phone" placeholder="e.g. +1 234 567 890">

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

.form-control:focus-visible {
    border-color: var(--Marine-blue);
}

.errorInput {
    border-color: var(--Strawberry-red);
    outline: none;
}

label {
    display: flex;
    justify-content: space-between;
    gap: 15%;
    align-items: end;
}

.error-msg {
    color: var(--Strawberry-red);
    font-size: .8em;
    font-weight: 500;
}

.error-msg::first-letter {
    text-transform: capitalize;
}
</style>