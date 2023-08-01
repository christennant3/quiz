<template>
  <div class="max-w-3xl mx-auto bg-slate-50 p-6 rounded-lg shadow-lg">
    <h1>Quiz</h1>
    <p>Question {{ questionIndex + 1  }} / {{ questions.length }}</p>
    <p class="pb-8">Score: {{ score }} / {{ questions.length }}</p>
    <div v-if="visible.question">
      
      <div v-for="question, index in questions">
        <template v-if="questionIndex === index">
          <p class="text-2xl pb-4">{{ question.text }}</p>

          <div v-for="(option, index) in question.options">

            <button class="p-3 bg-stone-300 rounded w-full m-2 hover:bg-stone-400" @click="answer(option, index)" :disabled="isDisabled" :class="{ 'btn-disabled': isDisabled }">
              {{ option }}
            </button>

          </div>
        </template>


      </div>
    </div>

    <div v-show="visible.feedback">

      <p v-show="visible.correct" class="text-green-600 font-bold text-3xl pl-2 m-2">Correct!</p>
      <p v-show="visible.wrong" class="text-red-600 font-bold text-3xl pl-2 m-2">Wrong!</p>
    
    </div>

    <div v-show="visible.result">
      <p class="font-bold text-3xl pl-8 m-2">You got {{ score }} out of {{ questions.length }}</p>
    </div>

    <div class="flex justify-center">
      <button @click="nextBtn" v-show="visible.next"
        class="bg-green-600 p-2 rounded m-2 text-white w-1/2 hover:bg-green-700 mt-6 w-50 text-center">Next</button>

    </div>
    <p>Question {{ questionIndex + 1 }} / {{ questions.length }}</p>
    <p>Score: {{ score }} / {{ questions.length }}</p>
  </div>
</template>

<script setup>
import { useAuthStore } from '~/stores/useAuthStore'
const auth = useAuthStore();
const questionIndex = ref(0);
const score = ref(0);
const isDisabled = ref(false);
const visible = reactive([
  {
    next: false,
    feedback: false,
    result: false,
    correct: false,
    wrong: false,
    question: true
  }
]);
const questions = reactive([
  {
    text: 'What is the capital of France?',
    options: ['Paris', 'Berlin', 'Madrid', 'Rome'],
    correctIndex: 0
  },
  {
    text: 'Who is the creator of JavaScript?',
    options: ['Brendan Eich', 'Guido van Rossum', 'James Gosling', 'Dennis Ritchie'],
    correctIndex: 0
  },
  {
    text: 'Which HTML tag is used to display an image?',
    options: ['<image>', '<img>', '<pic>', '<photo>'],
    correctIndex: 1
  },
  {
    text: 'What is the most popular programming language in 2023?',
    options: ['Python', 'JavaScript', 'Java', 'C#'],
    correctIndex: 1
  }
])

onMounted(() => {
  visible.question = true;
  questions.sort(() => Math.random() - 0.5)
})

function answer(option, index) {

  if (index === questions[questionIndex.value].correctIndex) {
    // correct answer 
    score.value++
    visible.correct = true;
  } else {
    // wrong answer
    visible.wrong = true;
  }
  visible.next = true;
  visible.feedback = true;
  isDisabled.value = true;

}

function nextBtn() {
  visible.next = false;
  visible.correct = false;
  visible.wrong = false;
  isDisabled.value = false;

  questionIndex.value++

  if (questionIndex.value === questions.length) {
    visible.result = true;
    visible.next = false;
    visible.correct = false;
    visible.wrong = false;
    isDisabled.value = false;

  }
}

const totalQuestions = computed(() => questions.length);

</script>

<style scoped>
  button {
    cursor: pointer;
  }

  .btn-disabled {
    cursor: not-allowed;
  }

</style>

