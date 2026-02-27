<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { Thermometer, Snowflake, Wrench } from 'lucide-vue-next'

const heroImages = [
  '/aires/limpieza_aire.jpg',
  '/aires/llenado_gas_aire.jpg',
  '/aires/montado_aire.jpg',
  '/heladeras/reparando_nevera.jpg',
  '/heladeras/verificando_gas_nevera.jpg',
]

const currentHeroImageIndex = ref(0)
let heroInterval: ReturnType<typeof setInterval>

onMounted(() => {
  heroInterval = setInterval(() => {
    currentHeroImageIndex.value = (currentHeroImageIndex.value + 1) % heroImages.length
  }, 2000)
})

onUnmounted(() => {
  clearInterval(heroInterval)
})
</script>

<template>
  <div class="w-full">
    <section
      class="text-white py-24"
      :style="{
        backgroundImage: `linear-gradient(rgba(29, 78, 216, 0.75), rgba(37, 99, 235, 0.75)), url('${heroImages[currentHeroImageIndex]}')`,
        backgroundSize: 'cover',
        backgroundPosition: 'center',
        transition: 'background-image 0.6s ease-in-out',
      }"
    >
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-5xl md:text-6xl font-bold mb-4">Refrigeración Roberto</h1>
        <p class="text-xl md:text-2xl mb-6 text-gray-100">
          Servicio técnico profesional en refrigeración comercial y residencial
        </p>
        <p class="text-lg mb-8 text-gray-100 max-w-2xl">
          Especialistas en mantenimiento y reparación de aires acondicionados y neveras, con
          atención rápida, diagnóstico confiable y soluciones duraderas.
        </p>
        <div class="flex gap-4 flex-wrap">
          <RouterLink
            to="/servicios"
            class="bg-yellow-400 text-blue-700 px-8 py-3 rounded-lg font-bold hover:bg-yellow-500 transition-all duration-300"
          >
            Ver servicios
          </RouterLink>
          <RouterLink
            to="/contacto#formulario"
            class="border-2 border-white text-white px-8 py-3 rounded-lg font-bold hover:bg-white hover:text-blue-700 transition-all duration-300"
          >
            Solicitar visita técnica
          </RouterLink>
        </div>
      </div>
    </section>

    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-4xl font-bold text-blue-700 mb-10 text-center">¿Qué hacemos?</h2>
        <div class="grid md:grid-cols-3 gap-8">
          <div class="bg-white rounded-lg shadow-md overflow-hidden">
            <img
              src="/aires/limpieza_aire.jpg"
              alt="Limpieza de aire acondicionado"
              class="w-full h-48 object-cover"
            />
            <div class="p-8">
              <Thermometer :size="34" class="text-yellow-500 mb-4" />
              <h3 class="text-xl font-bold text-blue-700 mb-3">Mantenimiento Preventivo</h3>
              <p class="text-gray-700">
                Revisiones periódicas para evitar fallas, mejorar rendimiento y prolongar la vida
                útil de tus equipos de refrigeración.
              </p>
            </div>
          </div>
          <div class="bg-white rounded-lg shadow-md overflow-hidden">
            <img
              src="/heladeras/reparando_nevera.jpg"
              alt="Reparación de nevera"
              class="w-full h-48 object-cover"
            />
            <div class="p-8">
              <Wrench :size="34" class="text-yellow-500 mb-4" />
              <h3 class="text-xl font-bold text-blue-700 mb-3">Reparación Correctiva</h3>
              <p class="text-gray-700">
                Solución de averías en aires acondicionados y neveras con diagnóstico técnico y
                repuestos de calidad.
              </p>
            </div>
          </div>
          <div class="bg-white rounded-lg shadow-md overflow-hidden">
            <img
              src="/aires/llenado_gas_aire.jpg"
              alt="Carga de gas en aire acondicionado"
              class="w-full h-48 object-cover"
            />
            <div class="p-8">
              <Snowflake :size="34" class="text-yellow-500 mb-4" />
              <h3 class="text-xl font-bold text-blue-700 mb-3">Instalación y Puesta a Punto</h3>
              <p class="text-gray-700">
                Instalación segura y configuración óptima para asegurar eficiencia energética y
                funcionamiento estable.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4 text-center">
        <h2 class="text-4xl font-bold mb-6">Atención rápida y profesional</h2>
        <p class="text-lg mb-8 text-gray-100 max-w-2xl mx-auto">
          Coordinamos tu servicio y te acompañamos en todo el proceso para que tus equipos vuelvan a
          funcionar como corresponde.
        </p>
        <RouterLink
          to="/contacto#formulario"
          class="inline-block bg-yellow-400 text-blue-700 px-10 py-4 rounded-lg font-bold hover:bg-yellow-500 transition-all duration-300 hover:shadow-lg text-lg"
        >
          Contactar ahora
        </RouterLink>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
