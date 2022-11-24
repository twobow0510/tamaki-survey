<template>
    <div class="mb-2">{{ question.label }}</div>
    <div>
        <input :type="question.type" :name="`question${question.id}`"
            v-model="question.answer" @input="$emit('change-value', { val:$event.target.value, index:qIndex})">
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