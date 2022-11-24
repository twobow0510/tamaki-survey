<template>
    <div class="mb-2">{{ question.label }}</div>
    <div class="flex flex-rows flex-wrap items-center text-sm">
        <div v-for="(option, index) in question.options" :key="index" class="mr-4 mb-2">
            <input :type="question.type" :value="option.label" :name="`question${question.id}`"
                class="border border-gray-200"
                v-model="question.answer" @change="$emit('change-value', { val:$event.target.value, index:qIndex})">
            <label class="ml-2">{{ option.label }}</label>
        </div>
    </div>
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