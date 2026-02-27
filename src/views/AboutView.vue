<script setup lang="ts">
import { Award, Wrench, ShieldCheck, Clock3 } from 'lucide-vue-next'
</script>

<template>
  <div class="w-full">
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <div class="flex items-center gap-4 mb-4">
          <img src="/logo.png" alt="Refrigeración Roberto" class="h-16 w-auto" />
          <h1 class="text-4xl md:text-5xl font-bold">Nosotros</h1>
        </div>
        <p class="text-xl mt-4 text-gray-100">
          Refrigeración Roberto: experiencia, compromiso y confianza
        </p>
      </div>
    </section>

    <section class="py-16 bg-white">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-8">Nuestra Empresa</h2>
        <div class="grid md:grid-cols-2 gap-8 items-stretch">
          <img
            src="/aires/llenado_gas_aire.jpg"
            alt="Servicio técnico de aire acondicionado"
            class="w-full h-full min-h-[260px] object-cover rounded-lg shadow-md"
          />
          <div class="bg-blue-50 p-8 rounded-lg border-l-4 border-yellow-400">
            <p class="text-gray-700 text-lg leading-relaxed mb-4">
              En Refrigeración Roberto nos dedicamos al mantenimiento y reparación de sistemas de
              aire acondicionado y neveras en hogares, comercios y oficinas.
            </p>
            <p class="text-gray-700 text-lg leading-relaxed">
              Trabajamos con atención responsable, diagnósticos precisos y soluciones prácticas para
              que cada cliente recupere el confort y la continuidad de sus equipos.
            </p>
          </div>
        </div>
      </div>
    </section>

    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-12 text-center">Nuestros Valores</h2>
        <div class="grid md:grid-cols-4 gap-6">
          <div class="bg-white rounded-lg shadow-md p-6 text-center">
            <Award :size="42" class="text-yellow-500 mx-auto mb-3" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Calidad</h3>
            <p class="text-gray-700">
              Cada servicio se realiza con estándar técnico y revisión final.
            </p>
          </div>
          <div class="bg-white rounded-lg shadow-md p-6 text-center">
            <Wrench :size="42" class="text-yellow-500 mx-auto mb-3" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Profesionalismo</h3>
            <p class="text-gray-700">
              Atención clara, ordenada y enfocada en resolver el problema.
            </p>
          </div>
          <div class="bg-white rounded-lg shadow-md p-6 text-center">
            <ShieldCheck :size="42" class="text-yellow-500 mx-auto mb-3" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Confianza</h3>
            <p class="text-gray-700">
              Servicio transparente y recomendaciones honestas para cada equipo.
            </p>
          </div>
          <div class="bg-white rounded-lg shadow-md p-6 text-center">
            <Clock3 :size="42" class="text-yellow-500 mx-auto mb-3" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Puntualidad</h3>
            <p class="text-gray-700">
              Cumplimos tiempos de visita y respuesta según cada urgencia.
            </p>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4 text-center">
        <h2 class="text-3xl font-bold mb-8">Nuestra Misión</h2>
        <div class="bg-blue-600 p-8 rounded-lg text-center max-w-4xl mx-auto">
          <p class="text-xl leading-relaxed">
            Brindar soluciones de refrigeración confiables, rápidas y eficientes para que cada
            cliente tenga sus equipos funcionando en óptimas condiciones durante todo el año.
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
