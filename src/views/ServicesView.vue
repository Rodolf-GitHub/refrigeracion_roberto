<script setup lang="ts">
import { ref } from 'vue'

const services = ref([
  {
    title: 'Mantenimiento de Aires Acondicionados',
    icon: '❄️',
    image: '/aires/limpieza_aire.jpg',
    items: [
      'Limpieza de unidad interna y externa',
      'Revisión de presión y carga de gas refrigerante',
      'Chequeo eléctrico y de drenaje',
      'Optimización de rendimiento y consumo',
    ],
  },
  {
    title: 'Reparación de Neveras',
    icon: '🧊',
    image: '/heladeras/reparando_nevera.jpg',
    items: [
      'Diagnóstico de fallas de enfriamiento',
      'Cambio de componentes dañados',
      'Corrección de fugas y recargas',
      'Ajuste de termostato y sistema de arranque',
    ],
  },
  {
    title: 'Instalación y Servicio Técnico',
    icon: '🛠️',
    image: '/heladeras/verificando_gas_nevera.jpg',
    items: [
      'Instalación de equipos nuevos',
      'Desinstalación y reinstalación segura',
      'Asesoría para elegir capacidad adecuada',
      'Atención a hogares, oficinas y comercios',
    ],
  },
])
</script>

<template>
  <div class="w-full">
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Servicios</h1>
        <p class="text-xl mt-4 text-gray-100">
          Mantenimiento y reparación de aire acondicionado y neveras
        </p>
      </div>
    </section>

    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <div class="grid md:grid-cols-3 gap-8">
          <div
            v-for="(service, index) in services"
            :key="index"
            class="bg-white rounded-lg shadow-md overflow-hidden"
          >
            <img :src="service.image" :alt="service.title" class="w-full h-52 object-cover" />
            <div class="bg-gradient-to-r from-blue-700 to-blue-500 p-6 text-white">
              <h2 class="text-2xl font-bold flex items-center gap-3">
                <span class="text-4xl">{{ service.icon }}</span>
                {{ service.title }}
              </h2>
            </div>
            <div class="p-6">
              <ul class="space-y-3">
                <li
                  v-for="(item, itemIndex) in service.items"
                  :key="itemIndex"
                  class="text-gray-700 flex gap-2"
                >
                  <span class="text-yellow-500 font-bold">•</span>
                  <span>{{ item }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4 text-center">
        <h2 class="text-4xl font-bold mb-6">¿Necesitas asistencia técnica?</h2>
        <p class="text-xl mb-8 text-gray-100 max-w-2xl mx-auto">
          Te ayudamos a recuperar el funcionamiento de tus equipos con un servicio confiable y
          profesional.
        </p>
        <RouterLink
          to="/contacto#formulario"
          class="inline-block bg-yellow-400 text-blue-700 px-10 py-4 rounded-lg font-bold hover:bg-yellow-500 transition-all duration-300 hover:shadow-lg text-lg"
        >
          Solicitar servicio
        </RouterLink>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
