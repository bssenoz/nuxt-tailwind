<template>
  <div class="min-h-screen flex items-start justify-center bg-gray-100">
    <div class="flex flex-col">
      <div class="p-8 bg-white rounded-lg shadow-md mt-8">
        <h1 class="text-lg font-bold text-gray-800">Performans Testi - Tailwind</h1>
        <p class="text-gray-600">Buton ve Tooltip ile.</p>
        <div class="mt-6 space-x-4">
          <button @click="clicked = !clicked" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            {{ clicked ? 'Tıklama Bırak' : 'Tıkla' }}
          </button>
          <button @mouseenter="showTooltip = true" @mouseleave="showTooltip = false" class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded relative">
            Tooltip'li Buton
            <div v-if="showTooltip" class="absolute mt-2 left-1/2 transform -translate-x-1/2 px-2 py-1 bg-gray-700 text-white rounded">
              Bu bir tooltip.
            </div>
          </button>
          <button @click="dialogOpen = true" class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">
            Dialog Aç
          </button>
        </div>
      </div>

      <!-- Tabs Section -->
      <div class="mt-8 p-8 bg-white rounded-lg shadow-md">
        <div class="flex border-b border-gray-300">
          <button @click="tab = 0" class="py-2 px-4" :class="tab === 0 ? 'text-blue-600 border-b-2 border-blue-600' : 'text-gray-600'">Tab 1</button>
          <button @click="tab = 1" class="py-2 px-4" :class="tab === 1 ? 'text-blue-600 border-b-2 border-blue-600' : 'text-gray-600'">Tab 2</button>
          <button @click="tab = 2" class="py-2 px-4" :class="tab === 2 ? 'text-blue-600 border-b-2 border-blue-600' : 'text-gray-600'">Tab 3</button>
        </div>
        <div class="mt-4">
          <div v-if="tab === 0" class="text-gray-800">Tab 1 içeriği burada.</div>
          <div v-if="tab === 1" class="text-gray-800">Tab 2 içeriği burada.</div>
          <div v-if="tab === 2" class="text-gray-800">Tab 3 içeriği burada.</div>
        </div>
      </div>

      <!-- Carousel Section -->
      <div class="mt-8 p-8 bg-white rounded-lg shadow-md">
        <h2 class="text-lg font-bold text-gray-800">Carousel</h2>
        <div class="relative">
          <div class="overflow-hidden">
            <div class="flex transition-transform duration-500" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
              <div class="min-w-full">
                <img src="https://via.placeholder.com/400x200?text=Slide+1" alt="Slide 1" class="w-full h-48 object-cover rounded-lg" />
              </div>
              <div class="min-w-full">
                <img src="https://via.placeholder.com/400x200?text=Slide+2" alt="Slide 2" class="w-full h-48 object-cover rounded-lg" />
              </div>
              <div class="min-w-full">
                <img src="https://via.placeholder.com/400x200?text=Slide+3" alt="Slide 3" class="w-full h-48 object-cover rounded-lg" />
              </div>
            </div>
          </div>
          <button @click="prevSlide" class="absolute left-0 top-1/2 transform -translate-y-1/2 bg-white rounded-full p-2 shadow-md">
            &#10094;
          </button>
          <button @click="nextSlide" class="absolute right-0 top-1/2 transform -translate-y-1/2 bg-white rounded-full p-2 shadow-md">
            &#10095;
          </button>
        </div>
      </div>

      <!-- Form Section -->
      <div class="mt-8 p-8 bg-white rounded-lg shadow-md">
        <h2 class="text-lg font-bold text-gray-800">İletişim Formu</h2>
        <form @submit.prevent="submitForm">
          <div class="mt-4">
            <label class="block text-gray-700" for="name">Adınız:</label>
            <input v-model="name" type="text" id="name" required class="mt-1 block w-full border border-gray-300 rounded-lg p-2" />
          </div>
          <div class="mt-4">
            <label class="block text-gray-700" for="email">E-posta:</label>
            <input v-model="email" type="email" id="email" required class="mt-1 block w-full border border-gray-300 rounded-lg p-2" />
          </div>
          <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4">Gönder</button>
        </form>
      </div>
    </div>

    <transition name="fade">
      <div v-if="dialogOpen" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
        <div class="bg-white rounded-lg p-6 w-1/3">
          <h2 class="text-lg font-bold text-gray-800">Dialog Başlığı</h2>
          <p class="text-gray-600">Bu bir dialog bileşenidir. Burada içerik ekleyebilirsin.</p>
          <button @click="dialogOpen = false" class="bg-blue-600 hover:bg-blue-700 text-white py-2 px-4 rounded mt-4">
            Kapat
          </button>
        </div>
      </div>
    </transition>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const clicked = ref(false);
const showTooltip = ref(false);
const dialogOpen = ref(false);
const tab = ref(0);

// Carousel state
const currentIndex = ref(0);
const name = ref('');
const email = ref('');

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % 3; // 3 slides
};

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + 3) % 3; // 3 slides
};

const submitForm = () => {
  alert(`Ad: ${name.value}, E-posta: ${email.value}`);
  name.value = '';
  email.value = '';
};
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to  {
  opacity: 0;
}
</style>
