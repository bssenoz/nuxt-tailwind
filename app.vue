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

      <div class="flex items-start justify-center bg-gray-100 mt-4">
    <div class="flex flex-col">
      <!-- Accordion Section -->
      <div class="mt-8 p-8 bg-white rounded-lg shadow-md w-96 h-72">
        <h2 class="text-lg font-bold text-gray-800">Accordion Bileşeni</h2>

        <div class="mt-4">
          <button @click="toggleAccordion(0)" class="w-full text-left py-3 px-4 font-bold bg-blue-600 text-white rounded">
            Accordion Başlık 1
          </button>
          <div v-if="activeAccordion === 0" class="p-4 bg-gray-100 rounded border border-gray-200 mt-2 overflow-y-auto h-32">
            Accordion içeriği 1 burada.
          </div>
        </div>

        <div class="mt-4">
          <button @click="toggleAccordion(1)" class="w-full text-left py-3 px-4 font-bold bg-blue-600 text-white rounded">
            Accordion Başlık 2
          </button>
          <div v-if="activeAccordion === 1" class="p-4 bg-gray-100 rounded border border-gray-200 mt-2 overflow-y-auto h-32">
            Accordion içeriği 2 burada.
          </div>
        </div>

        <div class="mt-4">
          <button @click="toggleAccordion(2)" class="w-full text-left py-3 px-4 font-bold bg-blue-600 text-white rounded">
            Accordion Başlık 3
          </button>
          <div v-if="activeAccordion === 2" class="p-4 bg-gray-100 rounded border border-gray-200 mt-2 overflow-y-auto h-32">
            Accordion içeriği 3 burada.
          </div>
        </div>
      </div>
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

const name = ref('');
const email = ref('');

const submitForm = () => {
  alert(`Ad: ${name.value}, E-posta: ${email.value}`);
  name.value = '';
  email.value = '';
};

const activeAccordion = ref<number | null>(null);

const toggleAccordion = (index: number) => {
  activeAccordion.value = activeAccordion.value === index ? null : index;
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
