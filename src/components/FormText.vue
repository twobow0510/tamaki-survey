<template>
    <div class="mb-2" v-if="question.label">{{ question.label }}</div>
    <div :class="{'w-full': question.placeholder}">
        <input :type="question.type" :name="`question${question.id}`"
            class="w-full text-sm form-input" :disabled="question.isDisable" :placeholder="question.placeholder"
            v-model="question.answer" @input="$emit('change-value', $event.target.value)">
        <!--@input="$emit('change-value', { val:$event.target.value, index:qIndex})"-->
    </div>
</template>

<script setup>
import { toRefs } from 'vue'

const props = defineProps({
    question: Object,
})
const { question } = toRefs(props)

//console.log(question.value.label)
const emit = defineEmits([
    'change-value'
])
</script>