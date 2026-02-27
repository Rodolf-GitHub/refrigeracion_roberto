<script setup lang="ts">
import { ref } from 'vue'
import { MapPin, Phone, Mail } from 'lucide-vue-next'

const formData = ref({
  name: '',
  email: '',
  phone: '',
  message: '',
})

const handleSubmit = () => {
  const message = `Nombre: ${formData.value.name}%0AEmail: ${formData.value.email}%0ATeléfono: ${formData.value.phone}%0AMensaje: ${formData.value.message}`
  window.open(
    `mailto:labradaroberto23@gmail.com?subject=Consulta Refrigeración Roberto&body=${message}`,
  )
}
</script>

<template>
  <div class="w-full">
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Contacto</h1>
        <p class="text-xl mt-4 text-gray-100">
          Estamos listos para ayudarte con tus equipos de refrigeración
        </p>
      </div>
    </section>

    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-12 text-center">Información de Contacto</h2>

        <div class="grid md:grid-cols-2 gap-8 mb-12">
          <div class="bg-white rounded-lg shadow-md p-8 text-center">
            <div
              class="w-20 h-20 bg-yellow-400 rounded-full flex items-center justify-center mx-auto mb-4"
            >
              <Phone :size="40" class="text-blue-700" />
            </div>
            <h3 class="text-2xl font-bold text-blue-700 mb-2">Teléfono</h3>
            <a href="tel:+59892698549" class="text-yellow-400 font-bold text-lg hover:underline"
              >+598 92 698 549</a
            >
          </div>

          <div class="bg-white rounded-lg shadow-md p-8 text-center">
            <div
              class="w-20 h-20 bg-yellow-400 rounded-full flex items-center justify-center mx-auto mb-4"
            >
              <Mail :size="40" class="text-blue-700" />
            </div>
            <h3 class="text-2xl font-bold text-blue-700 mb-2">Email</h3>
            <a
              href="mailto:labradaroberto23@gmail.com"
              class="text-yellow-400 font-bold text-lg hover:underline break-all"
              >labradaroberto23@gmail.com</a
            >
          </div>
        </div>

        <div class="bg-white rounded-lg shadow-md p-8 mb-12">
          <div class="flex items-start gap-4">
            <MapPin :size="32" class="text-yellow-400 flex-shrink-0 mt-1" />
            <div>
              <h3 class="text-2xl font-bold text-blue-700 mb-2">Dirección</h3>
              <p class="text-gray-700 text-lg">Montevideo, Uruguay</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="formulario" class="py-16 bg-white">
      <div class="max-w-2xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-8 text-center">Solicitar Servicio</h2>

        <form @submit.prevent="handleSubmit" class="bg-blue-50 rounded-lg p-8 shadow-md">
          <div class="mb-6">
            <label class="block text-blue-700 font-bold mb-2">Nombre completo *</label>
            <input
              v-model="formData.name"
              type="text"
              required
              class="w-full px-4 py-2 border-2 border-blue-200 rounded-lg focus:border-blue-700 focus:outline-none transition-colors"
              placeholder="Tu nombre"
            />
          </div>

          <div class="grid md:grid-cols-2 gap-6 mb-6">
            <div>
              <label class="block text-blue-700 font-bold mb-2">Email *</label>
              <input
                v-model="formData.email"
                type="email"
                required
                class="w-full px-4 py-2 border-2 border-blue-200 rounded-lg focus:border-blue-700 focus:outline-none transition-colors"
                placeholder="tu@email.com"
              />
            </div>
            <div>
              <label class="block text-blue-700 font-bold mb-2">Teléfono</label>
              <input
                v-model="formData.phone"
                type="tel"
                class="w-full px-4 py-2 border-2 border-blue-200 rounded-lg focus:border-blue-700 focus:outline-none transition-colors"
                placeholder="Teléfono de contacto"
              />
            </div>
          </div>

          <div class="mb-6">
            <label class="block text-blue-700 font-bold mb-2">Mensaje *</label>
            <textarea
              v-model="formData.message"
              required
              rows="6"
              class="w-full px-4 py-2 border-2 border-blue-200 rounded-lg focus:border-blue-700 focus:outline-none transition-colors resize-none"
              placeholder="Describe tu equipo y la falla que presenta..."
            ></textarea>
          </div>

          <button
            type="submit"
            class="w-full bg-yellow-400 text-blue-700 font-bold py-3 rounded-lg hover:bg-yellow-500 transition-all duration-300 hover:shadow-lg text-lg"
          >
            Enviar Solicitud
          </button>
        </form>

        <p class="text-center text-gray-600 mt-6 text-sm">
          * Campos obligatorios. Nos pondremos en contacto pronto.
        </p>
      </div>
    </section>

    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4 text-center">
        <h2 class="text-4xl font-bold mb-6">Atención técnica de confianza</h2>
        <p class="text-xl mb-8 text-gray-100 max-w-2xl mx-auto">
          Coordinamos visitas técnicas para mantenimiento, reparación e instalación de equipos de
          refrigeración, ajustándonos a tus necesidades y horarios.
        </p>
        <p class="text-lg text-yellow-400">Gracias por confiar en Refrigeración Roberto.</p>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
