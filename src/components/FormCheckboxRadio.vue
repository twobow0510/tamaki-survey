<template>
    <div class="mb-2">{{ question.label }}</div>
    <div class="flex space-x-4 flex-wrap">
        <div v-for="(option, index) in question.options" :key="index">
            <input :type="question.type" :value="option.label" :name="`question${question.id}`"
                v-model="question.answer" @change="$emit('change-value', { val:$event.target.value, index:qIndex})">
            <label class="ml-2">{{ option.label }}</label>
        </div>
    </div>
    <div>{{ question.answer }}</div>
</template>

<script setup>
import { toRefs } from 'vue'

const props = defineProps({
    question: Object,
    qIndex: Number,
})
const { question, qIndex } = toRefs(props)

const emit = defineEmits([
    'change-value'
])
</script>