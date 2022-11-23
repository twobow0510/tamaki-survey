<template>
    <div class="mb-2">{{ question.label }}</div>
    <select v-model="question.answer">
        <option value="">選択して下さい</option>
        <option v-for="(option, index) in question.options" :key="index"
            :value="option.label"
        >{{ option.label }}</option>
    </select>
</template>

<script setup>
import { toRefs } from 'vue'

const props = defineProps({
    question: Object,
})
const { question } = toRefs(props)
</script>