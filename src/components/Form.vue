<script setup lang="ts">
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

</script>

<template>
    <form>
        <Step1 v-if="props.step == 1" />
        <Step2 v-else-if="props.step == 2" />
        <Step3 v-else-if="props.step == 3" />
        <Step4 v-else-if="props.step == 4" />
    </form>
</template>