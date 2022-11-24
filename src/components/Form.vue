<template>
    <form @submit.prevent="submit" class="text-left space-y-8">
        <div v-for="(question, index) in map_questions" :key="question.id">
            <form-text v-if="question.type == 'text'"
                :question="question" :qIndex="index" @changeValue="update" />
            <form-checkbox-radio v-else-if="question.type == 'radio' || question.type == 'checkbox'"
                :question="question" :qIndex="index" @changeValue="update" />
            <form-selectbox v-else-if="question.type == 'selectbox'"
                :question="question" :qIndex="index" @changeValue="update" />
        </div>
        <button class="">送信する</button>
    </form>

</template>

<script setup>
import { ref, toRefs, computed, reactive, onMounted } from 'vue'
import liff from '@line/liff';
import FormText from '@/components/FormText.vue'
import FormCheckboxRadio from '@/components/FormCheckboxRadio.vue'
import FormSelectbox from '@/components/FormSelectbox.vue'

onMounted(() => {
    liff.init({
        liffId: '1657367036-Y9qj9ENd',
    });
    console.log(map_questions.value)
})

const update = (arg) => {
    console.log(arg)
}

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

const questions = ref([
    {
        id: 1,
        type: 'radio',
        label: 'ジェネリック希望しますか？',
        options: [
            {
                label: '希望する',
            },
            {
                label: '希望しない',
            },
        ],
        required: true,
    },
    {
        id: 2,
        type: 'radio',
        label: '薬で副作用が起きたことがありますか？',
        options: [
            {
                label: 'いいえ',
            },
            {
                label: 'はい',
            },
        ],
        required: true,
        hasNext: true,
        sub: '「はい」と回答した場合、次の質問にお答えください',
    },
    {
        id: 3,
        type: 'text',
        label: '薬の名前と症状をご記入ください',
        required: true,
    },
    {
        id: 4,
        type: 'checkbox',
        label: 'アレルギーはありますか？',
        options: [
            {
                label: '特になし',
            },
            {
                label: '卵',
            },
            {
                label: '牛乳',
            },
            {
                label: 'ダニ',
            },
            {
                label: 'ハウスダスト',
            },
            {
                label: '金属',
            },
            {
                label: '花粉',
            },
            {
                label: 'その他',
            },
        ],
        required: true,
    },
    {
        id: 5,
        type: 'checkbox',
        label: 'ご自身にあてはまる体質はありますか？',
        options: [
            {
                label: '特になし',
            },
            {
                label: '下痢しやすい',
            },
            {
                label: '便秘しやすい',
            },
            {
                label: '胃が弱い',
            },
            {
                label: '眠れない',
            },
            {
                label: 'かぶれやすい',
            },
            {
                label: 'その他',
            },
        ],
        required: true,
    },
    {
        id: 6,
        type: 'checkbox',
        label: '今までにかかった病気、または治療中の病気はありますか？',
        options: [
            {
                label: '特になし',
            },
            {
                label: '胃、十二指腸潰瘍',
            },
            {
                label: '高血圧',
            },
            {
                label: '糖尿病',
            },
            {
                label: '心疾患',
            },
            {
                label: '脳血管障害',
            },
            {
                label: '肝臓病',
            },
            {
                label: '腎臓病',
            },
            {
                label: '喘息',
            },
            {
                label: '緑内障',
            },
            {
                label: '前立腺疾患',
            },
            {
                label: '甲状腺疾患',
            },
            {
                label: 'リウマチ',
            },
            {
                label: '骨粗鬆症',
            },
            {
                label: '癌',
            },
            {
                label: 'その他',
            },
        ],
        required: true,
    },
    {
        id: 7,
        type: 'radio',
        label: '他にかかっている病院ありますか？',
        options: [
            {
                label: 'いいえ',
            },
            {
                label: 'はい',
            },
        ],
        required: true,
        hasNext: true,
        sub: '「はい」と回答した場合、次の質問にお答えください',
    },
    {
        id: 8,
        type: 'text',
        label: '病院名をご記入ください',
        required: true,
    },
    {
        id: 9,
        type: 'radio',
        label: '服用中の薬はありますか？',
        options: [
            {
                label: 'いいえ',
            },
            {
                label: 'はい',
            },
        ],
        required: true,
        hasNext: true,
        sub: '「はい」と回答した場合、次の質問にお答えください',
    },
    {
        id: 10,
        type: 'text',
        label: 'お薬手帳をご提示くださるか薬名をご記入ください',
        required: true,
    },
    {
        id: 11,
        type: 'radio',
        label: '服用中のサプリメントはありますか？',
        options: [
            {
                label: 'いいえ',
            },
            {
                label: 'はい',
            },
        ],
        required: true,
        hasNext: true,
        sub: '「はい」と回答した場合、次の質問にお答えください',
    },
    {
        id: 12,
        type: 'text',
        label: '製品名をご記入ください',
        required: true,
    },
    {
        id: 13,
        type: 'radio',
        label: 'タバコは吸われますか？',
        options: [
            {
                label: 'いいえ',
            },
            {
                label: 'はい',
            },
        ],
        required: true,
    },
    {
        id: 14,
        type: 'radio',
        label: 'お酒は飲まれますか？',
        options: [
            {
                label: '飲まない',
            },
            {
                label: '毎日飲む',
            },
            {
                label: 'ときどき飲む',
            },
        ],
        required: true,
    },
    {
        id: 15,
        type: 'radio',
        label: '(女性のみ)妊娠もしくは授乳中ですか？',
        options: [
            {
                label: 'いいえ',
            },
            {
                label: 'わからない',
            },
            {
                label: 'はい',
            },
        ],
        required: true,
        hasNext: true,
        sub: '「はい」と回答した場合、次の質問にお答えください',
    },
    {
        id: 16,
        type: 'selectbox',
        label: '妊娠/生後',
        options: [
            {
                label: 1,
            },
            {
                label: 2,
            },
            {
                label: 3,
            },
            {
                label: 4,
            },
            {
                label: 5,
            },
            {
                label: 6,
            },
            {
                label: 7,
            },
            {
                label: 8,
            },
            {
                label: 9,
            },
            {
                label: 10,
            },
        ],
        required: true,
    },

])

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


