<template>
  <div class="image-uploader">
    <div class="border-2 border-dashed border-gray-300 p-4 text-center cursor-pointer" @click="triggerFileInput">
      <input type="file" ref="fileInput" @change="handleFileChange" class="hidden" accept="image/png,image/jpeg" multiple>
      <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 mx-auto text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
      </svg>
    </div>
    <div class="uploaded-images mt-4 grid grid-cols-3 gap-4">
      <div v-for="(image, index) in previewImages" :key="index" class="relative group">
        <img :src="image" class="w-full h-full object-cover rounded" />
        <div class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity">
          <button @click="viewImage(image)" class="text-white p-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 10l4.553-4.553A2 2 0 0017.13 3H6.87a2 2 0 00-1.424.553L9 10M9 21h6M9 14h6m-3-3v3m-1 4h2" />
            </svg>
          </button>
          <button @click="removeImage(index)" class="text-white p-2 ml-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>
    <Modal v-if="showModal" @close="showModal = false">
      <img :src="selectedImage" class="w-full h-full object-cover rounded" />
    </Modal>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Modal from './Modal.vue';

const fileInput = ref(null);
const images = ref([]);
const previewImages = ref([]);
const showModal = ref(false);
const selectedImage = ref('');

const emit = defineEmits(['update:modelValue']);

function triggerFileInput() {
  fileInput.value.click();
}

function handleFileChange(event) {
  const files = event.target.files;
  const fileArray = Array.from(files);
  images.value.push(...fileArray);
  updatePreviewImages();
  emit('update:modelValue', images.value);
}

function updatePreviewImages() {
  previewImages.value = images.value.map(file => URL.createObjectURL(file));
}

function viewImage(image) {
  selectedImage.value = image;
  showModal.value = true;
}

function removeImage(index) {
  images.value.splice(index, 1);
  updatePreviewImages();
  emit('update:modelValue', images.value);
}
</script>

<style scoped>
.image-uploader {
  position: relative;
}

.uploaded-images img {
  transition: transform 0.2s ease-in-out;
}

.uploaded-images .group:hover img {
  transform: scale(1.1);
}

.uploaded-images .group {
  position: relative;
}

.uploaded-images .group .absolute {
  background-color: rgba(0, 0, 0, 0.5);
}
</style>
