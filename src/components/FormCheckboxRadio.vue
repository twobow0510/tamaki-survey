<template>
    <div class="mb-2">{{ question.label }}</div>
    <div class="flex space-x-4 flex-wrap">
        <div v-for="(option, index) in question.options" :key="index">
            <input :type="question.type" :value="option.label" v-model="question.answer">
            <label class="ml-2">{{ option.label }}</label>
        </div>
    </div>
    <div>{{ question.answer }}</div>
</template>

<script setup>
import { toRefs } from 'vue'

const props = defineProps({
    question: Object,
})
const { question } = toRefs(props)
</script>