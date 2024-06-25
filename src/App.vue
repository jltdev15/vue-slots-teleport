<template>
  <div>
    <header class="flex justify-center gap-3 flex-col">
      <h1 class="text-center p-6 text-3xl font-bold">Vue 3 Slots and Teleport Demo</h1>
      <button class="btn w-32 mx-auto" @click="toggleModal">Open modal</button>
      <button class="btn w-64 mx-auto" @click="toggleEmailModal">Open Email Modal</button>
    </header>
    <!-- First Modal -->
    <Modal :show="isModalShow" @toggleBackdrop="toggleBackdropHandler">
      <!-- First Slot -->
      <template #modal-header>
        <h3 class="text-lg font-bold">Hello!</h3>
      </template>

      <!-- Second Slot -->
      <template #modal-content>
        <p class="py-4">Press ESC key or click the button below to close</p>
      </template>

      <!-- Last Slot Action -->
      <template #default>
        <div class="modal-action">
          <form method="dialog">
            <!-- if there is a button in form, it will close the modal -->
            <button class="btn" @click="toggleModal">Close</button>
          </form>
        </div>
      </template>

    </Modal>


    <!-- Second modal -->
    <Modal :show="isModalInputShow" @toggleBackdrop="toggleBackdropHandler">
      <template #modal-header>
        Enter your Email Address to Subscribe
      </template>
      <template #modal-content>
        <label class="input input-bordered flex items-center gap-2">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="currentColor" class="h-4 w-4 opacity-70">
            <path
              d="M2.5 3A1.5 1.5 0 0 0 1 4.5v.793c.026.009.051.02.076.032L7.674 8.51c.206.1.446.1.652 0l6.598-3.185A.755.755 0 0 1 15 5.293V4.5A1.5 1.5 0 0 0 13.5 3h-11Z" />
            <path
              d="M15 6.954 8.978 9.86a2.25 2.25 0 0 1-1.956 0L1 6.954V11.5A1.5 1.5 0 0 0 2.5 13h11a1.5 1.5 0 0 0 1.5-1.5V6.954Z" />
          </svg>
          <input type="text" class="grow" placeholder="Email" />
        </label>
      </template>
      <template #default>
        <button class="btn bg-red-600 text-gray-50" @click="closeEmailModal">Cancel</button>
        <button class="btn btn-primary" @click="toggleModal">Submit</button>

      </template>


    </Modal>



  </div>
</template>

<script setup>

import { ref } from 'vue'
import Modal from './components/Modal.vue'
const isModalShow = ref(false)
const isModalInputShow = ref(false)
const toggleModal = () => {
  isModalShow.value = !isModalShow.value
}
const toggleEmailModal = () => {
  isModalInputShow.value = true;
}
const closeEmailModal = () => {
  isModalInputShow.value = false;
}

const toggleBackdropHandler = (payload) => {
  isModalShow.value = !payload;
  isModalInputShow.value = !payload;
}
</script>