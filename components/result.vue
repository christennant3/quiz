<template>
    <p class="font-bold text-3xl pl-8 m-2">You got {{ score }} out of {{ totalQuestions }}</p>
</template>

<script setup>
    const { questionIndex, totalQuestions } = defineProps({
    score: Number,
    totalQuestions: Number
})
</script>

<style lang="scss" scoped>

</style>