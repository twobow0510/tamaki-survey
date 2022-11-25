<template>
    <div class="mb-2">{{ question.label }}</div>
    <div class="flex flex-rows flex-wrap items-center text-sm">
        <div v-for="(option, index) in question.options" :key="index" class="mr-4 mb-2">
            <input :type="question.type" :value="option.label" :name="`question${question.id}`"
                :class="{'form-checkbox': question.type === 'checkbox', 'form-radio': question.type === 'radio'}"
                v-model="question.answer" @change="checkExtra(index)">
            <label class="ml-2">{{ option.label }}</label>
        </div>
        <form-text v-if="question.hasOther" :question="extraQuestion" @change-value="update" />
    </div>
    <!--<div>{{ question.answer }}</div>-->
</template>

<script setup>
import { ref, reactive, toRefs } from 'vue'
import { v4 as uuidv4 } from 'uuid'
import FormText from '@/components/FormText.vue'

const props = defineProps({
    question: Object,
    //qIndex: Number,
})
const { question } = toRefs(props)
const hasExtra = ref(false)

const extraQuestion = reactive({
    id: uuidv4(),
    type: 'text',
    label: '',
    required: true,
    isDisable: true,
    placeholder: 'その他を選択した場合は回答してください',
    answer: '',
})

const checkExtra = (index) => {
    //console.log(question.value.options.length - 1, index)
    if (question.value.options.length - 1 == index) {
        if (question.value.answer.length > 0) {
            question.value.answer = []
            question.value.answer.push('その他')
        }
    } else {
        if (question.value.answer.indexOf('その他') !== -1) {
            console.log(question.value.answer, question.value.answer.indexOf('その他'))
            question.value.answer = []
            question.value.answer.push(question.value.options[index].label)
        }
    }
    extraQuestion.isDisable = question.value.answer.indexOf('その他') !== -1 ? false: true
}

const update = (value) => {
    console.log(value)
    //question.value.answer = []
    question.value.answer.push(value)
    //question.value.answer.push(extraQuestion.answer)
}

//const emit = defineEmits([
//    'change-value'
//])
</script>