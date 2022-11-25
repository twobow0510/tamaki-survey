<template>
    <div class="p-4">
        <div class="mb-6 text-lg">問診票</div>
        <form @submit.prevent="submit" class="text-left space-y-8 text-slate-600">
            <div v-for="(question, index) in map_questions" :key="question.id">
                <form-text v-if="question.type == 'text'"
                    :question="question" />
                <form-checkbox-radio v-else-if="question.type == 'radio' || question.type == 'checkbox'"
                    :question="question" />
                <form-selectbox v-else-if="question.type == 'selectbox'"
                    :question="question" />
            </div>
            <div class="flex justify-center">
                <button class="rounded text-white bg-indigo-500 p-2">送信する</button>
            </div>
        </form>
    </div>
</template>

<script setup>
import { ref, toRefs, computed, reactive, onMounted } from 'vue'
import liff from '@line/liff';
import FormText from '@/components/FormText.vue'
import FormCheckboxRadio from '@/components/FormCheckboxRadio.vue'
import FormSelectbox from '@/components/FormSelectbox.vue'
import data from '../assets/data.json'

onMounted(() => {
    liff.init({
        liffId: '1657367036-Y9qj9ENd',
    });
    //console.log(data)
    //console.log(map_questions.value)
})

//const update = (arg) => {
//    console.log(arg)
//}

const submit = () => {
    let answer = ''
    console.log(form.questions)
    form.questions.forEach(question => {
        if (question.type === 'checkbox' && question.answer.length > 0 
            || question.type !== 'checkbox' && question.answer) {
            answer += question.label + '\n' + question.answer + '\n\n'
        }
    })

    liff
    .sendMessages([
    {
      type: "text",
      text: answer,
    },
  ])
  .then(() => {
    console.log("message sent")
    liff.closeWindow()
  })
  .catch((err) => {
    console.log("error", err);
  });
}

const questions = ref(data.questions)

const map_questions = computed(() => {
    return questions.value.map(question => {
        question['answer'] = question.type === 'checkbox' ? []: ''
        return question
    })
})

const form = reactive({
    questions: map_questions.value,
})

</script>


