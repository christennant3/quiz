<template>
  <div class="max-w-3xl mx-auto bg-slate-50 p-6 rounded-lg shadow-lg">
    <h1>Quiz</h1>

    <div v-for="question, index in questions">
      <template v-if="questionIndex === index">
        <p class="text-2xl pb-4">{{ question.text }}</p>

        <div v-for="(option, index) in question.options">
          
            <button class="p-3 bg-stone-300 rounded w-full m-2" @click="answer(option, index)">
            {{ option }}
            </button>

          
        </div>
      </template>


    </div>

    <div v-show="visible.feedback">

            <p v-show="visible.correct" class="text-green-600 font-bold text-xl pl-8 m-2">Correct!</p>
            <p v-show="visible.wrong" class="text-red-600 font-bold text-xl pl-8 m-2">Wrong!</p>
          
            <p>Score: {{ score }}</p>

          </div>

    <div class="flex justify-center">
      <button @click="nextBtn" v-show="visible.next"
        class="bg-green-600 p-2 rounded m-2 text-white w-1/2 hover:bg-green-700 mt-6 w-50 text-center">Next</button>

    </div>
  </div>
</template>

<script setup>
import { useAuthStore } from '~/stores/useAuthStore'
const auth = useAuthStore();
const questionIndex = ref(0);
const score = ref(0);
const visible = reactive([
  {
    next: false,
    feedback: false,
    result: false,
    correct: false,
    wrong: false
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
  
}

function nextBtn() {
  visible.next = false;
  visible.correct = false;
  visible.wrong = false;
  questionIndex.value++
}



</script>

<style lang="scss" scoped></style>

