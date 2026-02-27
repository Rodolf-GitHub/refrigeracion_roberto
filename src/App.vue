<script setup lang="ts">
import { RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'

const whatsappUrl =
  'https://wa.me/59892698549?text=Hola%20%22Refrigeracion%20Roberto%22%2C%20tengo%20un%20problema%20con%20uno%20de%20mis%20equipos.'
</script>

<template>
  <NavBar />
  <RouterView />
  <Footer />

  <a
    :href="whatsappUrl"
    target="_blank"
    rel="noopener noreferrer"
    aria-label="Abrir WhatsApp"
    class="fixed bottom-6 right-6 z-[60] h-14 w-14 rounded-full bg-green-500 shadow-lg hover:bg-green-600 transition-all duration-300 flex items-center justify-center"
  >
    <img
      src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg"
      alt="WhatsApp"
      class="h-8 w-8"
    />
  </a>
</template>

<style scoped></style>
