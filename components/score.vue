<template> 
     <p v-if="questionIndex < totalQuestions">Score: {{ score }} / {{ totalQuestions }}</p>
</template>

<script setup>
const { score, questions, questionIndex } = defineProps({
    score: Number,
    totalQuestions: Number,
    questionIndex: Number,
})
</script>