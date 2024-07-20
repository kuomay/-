<template>
  <div class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50">
    <div class="relative bg-white p-4 rounded shadow-lg max-w-3xl w-full">
      <button @click="$emit('close')" class="absolute top-4 right-4 text-black text-2xl z-10">
        &times;
      </button>
      <div class="relative">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fixed {
  position: fixed;
}
.absolute {
  position: absolute;
}
.z-10 {
  z-index: 10;
}
</style>
