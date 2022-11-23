<template>
    <div class="mb-2">{{ question.label }}</div>
    <div>
        <input :type="question.type" class="input">
    </div>
</template>

<script setup>
import { toRefs } from 'vue'

const props = defineProps({
    question: Object,
})
const { question } = toRefs(props)
</script>