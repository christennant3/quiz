<template>

    <p v-if="questionIndex < totalQuestions">Question {{ questionIndex + 1 }} / {{ totalQuestions }}</p>

</template>

<script setup>

    const { questionIndex, totalQuestions } = defineProps({
        questionIndex: Number,
        totalQuestions: Number
    })

</script>