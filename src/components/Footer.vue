<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { Phone, Mail, MapPin } from 'lucide-vue-next'
</script>

<template>
  <footer class="bg-blue-900 text-white mt-16">
    <div class="max-w-6xl mx-auto px-4 py-6">
      <div class="grid md:grid-cols-3 gap-6 mb-6">
        <div class="flex flex-col items-start gap-3">
          <h3 class="text-lg font-bold text-yellow-400">Refrigeración Roberto</h3>
          <p class="text-gray-300 text-xs">
            Especialistas en refrigeración, mantenimiento y reparación de aires acondicionados y
            neveras.
          </p>
        </div>

        <div>
          <h3 class="text-sm font-bold mb-2 text-yellow-400">Enlaces</h3>
          <nav class="space-y-1 text-xs">
            <div>
              <RouterLink to="/" class="text-gray-300 hover:text-yellow-400 transition"
                >Inicio</RouterLink
              >
            </div>
            <div>
              <RouterLink to="/nosotros" class="text-gray-300 hover:text-yellow-400 transition"
                >Nosotros</RouterLink
              >
            </div>
            <div>
              <RouterLink to="/servicios" class="text-gray-300 hover:text-yellow-400 transition"
                >Servicios</RouterLink
              >
            </div>
            <div>
              <RouterLink to="/proyectos" class="text-gray-300 hover:text-yellow-400 transition"
                >Proyectos</RouterLink
              >
            </div>
            <div>
              <RouterLink to="/contacto" class="text-gray-300 hover:text-yellow-400 transition"
                >Contacto</RouterLink
              >
            </div>
          </nav>
        </div>

        <div>
          <h3 class="text-sm font-bold mb-2 text-yellow-400">Contacto</h3>
          <div class="space-y-1 text-xs">
            <div class="flex items-center gap-2">
              <Phone :size="14" class="text-yellow-400" />
              <span class="text-gray-300">+598 92 698 549</span>
            </div>
            <div class="flex items-center gap-2">
              <Mail :size="14" class="text-yellow-400" />
              <a
                href="mailto:refrigeracionroberto@gmail.com"
                class="text-gray-300 hover:text-yellow-400 transition"
                >refrigeracionroberto@gmail.com</a
              >
            </div>
            <div class="flex items-start gap-2">
              <MapPin :size="14" class="text-yellow-400 flex-shrink-0 mt-0.5" />
              <span class="text-gray-300">Montevideo, Uruguay</span>
            </div>
          </div>
        </div>
      </div>

      <div
        class="border-t border-blue-700 pt-4 flex flex-col md:flex-row md:justify-between md:items-center gap-2 text-xs text-gray-300"
      >
        <p>&copy; 2026 Refrigeración Roberto. Todos los derechos reservados.</p>
        <p>Servicio técnico profesional en aire acondicionado y neveras</p>
      </div>
    </div>
  </footer>
</template>

<style scoped></style>
