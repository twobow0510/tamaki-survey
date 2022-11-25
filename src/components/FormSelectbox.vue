<template>
    <div class="mb-2">{{ question.label }}</div>
    <select :name="`question${question.id}`" v-model="question.answer"
        class="p-2 rounded text-sm form-select">
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
    //qIndex: Number,
})

const { question } = toRefs(props)

//const emit = defineEmits([
//    'change-value'
//])
</script>