<template>
  <div class="h-screen w-screen">
    <!-- ! -->
    <button @click="showFeedbackForm = true" class="fixed bottom-4 right-4 bg-blue-500 hover:bg-blue-600 text-white p-5 rounded-full shadow-lg">
      !
    </button>

    <!-- 表單彈窗 -->
    <FeedbackForm v-if="showFeedbackForm" @close="showFeedbackForm = false" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import FeedbackForm from './components/FeedbackForm.vue';

const showFeedbackForm = ref(false);
</script>
