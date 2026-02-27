<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { Phone, Mail, MapPin } from 'lucide-vue-next'
</script>

<template>
  <footer class="bg-blue-900 text-white mt-16">
    <div class="max-w-6xl mx-auto px-4 py-6">
      <div class="grid md:grid-cols-3 gap-6 mb-6">
        <!-- About -->
        <div class="flex flex-col items-start gap-3">
          <img src="/logo.png" alt="TecnoRaíz Logo" class="h-16 w-auto" />
          <p class="text-gray-300 text-xs">
            Servicios integrales en instalaciones eléctricas, automatismos y energías renovables.
          </p>
        </div>

        <!-- Quick Links -->
        <div>
          <h3 class="text-sm font-bold mb-2 text-yellow-400">Enlaces</h3>
          <nav class="space-y-1 text-xs">
            <div>
              <RouterLink to="/" class="text-gray-300 hover:text-yellow-400 transition"
                >Inicio</RouterLink
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

        <!-- Contact -->
        <div>
          <h3 class="text-sm font-bold mb-2 text-yellow-400">Contacto</h3>
          <div class="space-y-1 text-xs">
            <div class="flex items-center gap-2">
              <Phone :size="14" class="text-yellow-400" />
              <span class="text-gray-300">+598 094774616 / +598 094840059</span>
            </div>
            <div class="flex items-center gap-2">
              <Mail :size="14" class="text-yellow-400" />
              <a
                href="mailto:tecnoraizadm@gmail.com"
                class="text-gray-300 hover:text-yellow-400 transition"
                >tecnoraizadm@gmail.com</a
              >
            </div>
            <div class="flex items-start gap-2">
              <MapPin :size="14" class="text-yellow-400 flex-shrink-0 mt-0.5" />
              <span class="text-gray-300">León Pérez 3436</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom -->
      <div
        class="border-t border-blue-700 pt-4 flex flex-col md:flex-row md:justify-between md:items-center gap-2 text-xs text-gray-300"
      >
        <p>&copy; 2026 TecnoRaíz. Todos los derechos reservados.</p>
        <p>Diseñado con dedicación para tus proyectos</p>
      </div>
    </div>
  </footer>
</template>

<style scoped></style>
