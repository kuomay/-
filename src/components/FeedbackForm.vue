<template>
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div class="bg-white p-6 rounded-lg w-full max-w-md relative">
        <!-- 關閉按鈕 -->
        <button @click="emit('close')" class="absolute top-4 right-4 text-neutral-900 text-2xl">
          &times;
        </button>
  
        <h2 class="text-2xl font-bold mb-4 text-neutral-900">意見反饋</h2>
        
        <!-- 類別 -->
        <div class="mb-4">
          <label class="block mb-2 text-neutral-900">
            <span class="text-red-500">*</span> 類別
          </label>
          <select v-model="category" class="w-full p-2 border rounded text-neutral-900">
            <option class="text-neutral-900" value="">請選擇類別</option>
            <option class="text-neutral-900" value="bug">Bug報告</option>
            <option class="text-neutral-900" value="feature">功能建議</option>
            <option class="text-neutral-900" value="other">其他</option>
          </select>
        </div>
  
        <!-- 標題 -->
        <div class="mb-4">
          <label class="block mb-2 text-neutral-900">
            <span class="text-red-500">*</span> 標題(限30字符內)
          </label>
          <input v-model="title" type="text" class="w-full p-2 border rounded text-neutral-900" maxlength="30">
        </div>
  
        <!-- 描述 -->
        <div class="mb-4">
          <label class="block mb-2 text-neutral-900">
            <span class="text-red-500">*</span> 描述(限300字符內)
          </label>
          <textarea v-model="description" class="w-full p-2 border rounded text-neutral-900" rows="4" maxlength="300"></textarea>
        </div>
  
        <!-- 圖片上傳 -->
        <div class="mb-4">
          <label class="block mb-2 text-neutral-900">參考圖片(僅支持PNG、JPG格式，每張5MB內)</label>
          <ImageUploader class="text-neutral-900" v-model="images" />
        </div>
  
        <!-- 提交按鈕 -->
        <button @click="submitFeedback" class="bg-cyan-100 text-sky-400 p-2 rounded w-full">
          提交
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import ImageUploader from './ImageUploader.vue';
  
  const category = ref('');
  const title = ref('');
  const description = ref('');
  const images = ref([]);
  
  const emit = defineEmits(['close']);
  
  function submitFeedback() {
    console.log({ category: category.value, title: title.value, description: description.value, images: images.value });
    
    alert('提交成功！');
    
    // 5秒後自動關閉
    setTimeout(() => {
      emit('close');
    }, 5000);
  }
  </script>
  