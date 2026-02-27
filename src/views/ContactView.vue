<script setup lang="ts">
import { ref } from 'vue'
import { MapPin, Phone, Mail } from 'lucide-vue-next'

const formData = ref({
  name: '',
  email: '',
  phone: '',
  company: '',
  message: '',
})

const handleSubmit = () => {
  // Aquí puedes agregar la lógica para enviar el formulario
  const message = `Nombre: ${formData.value.name}%0AEmail: ${formData.value.email}%0ATeléfono: ${formData.value.phone}%0AEmpresa: ${formData.value.company}%0AMensaje: ${formData.value.message}`
  window.open(`mailto:tecnoraizadm@gmail.com?subject=Consulta TecnoRaíz&body=${message}`)
}
</script>

<template>
  <div class="w-full">
    <!-- Hero Section -->
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Contacto</h1>
        <p class="text-xl mt-4 text-gray-100">
          Estamos a tu disposición para responder tus consultas
        </p>
      </div>
    </section>

    <!-- Contact Information -->
    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-12 text-center">Información de Contacto</h2>

        <div class="grid md:grid-cols-3 gap-8 mb-12">
          <!-- Liesvy -->
          <div class="bg-white rounded-lg shadow-md p-8 text-center">
            <div
              class="w-20 h-20 bg-yellow-400 rounded-full flex items-center justify-center mx-auto mb-4"
            >
              <Phone :size="40" class="text-blue-700" />
            </div>
            <h3 class="text-2xl font-bold text-blue-700 mb-2">Ing. Liesvy Delgado</h3>
            <a href="tel:+598094840059" class="text-yellow-400 font-bold text-lg hover:underline"
              >+598 094840059</a
            >
          </div>

          <!-- Richard -->
          <div class="bg-white rounded-lg shadow-md p-8 text-center">
            <div
              class="w-20 h-20 bg-yellow-400 rounded-full flex items-center justify-center mx-auto mb-4"
            >
              <Phone :size="40" class="text-blue-700" />
            </div>
            <h3 class="text-2xl font-bold text-blue-700 mb-2">Ing. Richard Cruz</h3>
            <a href="tel:+598094774616" class="text-yellow-400 font-bold text-lg hover:underline"
              >+598 094774616</a
            >
          </div>

          <!-- Email -->
          <div class="bg-white rounded-lg shadow-md p-8 text-center">
            <div
              class="w-20 h-20 bg-yellow-400 rounded-full flex items-center justify-center mx-auto mb-4"
            >
              <Mail :size="40" class="text-blue-700" />
            </div>
            <h3 class="text-2xl font-bold text-blue-700 mb-2">Email</h3>
            <a
              href="mailto:tecnoraizadm@gmail.com"
              class="text-yellow-400 font-bold text-lg hover:underline break-all"
              >tecnoraizadm@gmail.com</a
            >
          </div>
        </div>

        <!-- Address -->
        <div class="bg-white rounded-lg shadow-md p-8 mb-12">
          <div class="flex items-start gap-4">
            <MapPin :size="32" class="text-yellow-400 flex-shrink-0 mt-1" />
            <div>
              <h3 class="text-2xl font-bold text-blue-700 mb-2">Dirección</h3>
              <p class="text-gray-700 text-lg">Leon Pérez 3436</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Form -->
    <section id="formulario" class="py-16 bg-white">
      <div class="max-w-2xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-8 text-center">Envíanos tu Consulta</h2>

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
            <label class="block text-blue-700 font-bold mb-2">Empresa</label>
            <input
              v-model="formData.company"
              type="text"
              class="w-full px-4 py-2 border-2 border-blue-200 rounded-lg focus:border-blue-700 focus:outline-none transition-colors"
              placeholder="Nombre de tu empresa"
            />
          </div>

          <div class="mb-6">
            <label class="block text-blue-700 font-bold mb-2">Mensaje *</label>
            <textarea
              v-model="formData.message"
              required
              rows="6"
              class="w-full px-4 py-2 border-2 border-blue-200 rounded-lg focus:border-blue-700 focus:outline-none transition-colors resize-none"
              placeholder="Cuéntanos sobre tu proyecto..."
            ></textarea>
          </div>

          <button
            type="submit"
            class="w-full bg-yellow-400 text-blue-700 font-bold py-3 rounded-lg hover:bg-yellow-500 transition-all duration-300 hover:shadow-lg text-lg"
          >
            Enviar Consulta
          </button>
        </form>

        <p class="text-center text-gray-600 mt-6 text-sm">
          * Campos obligatorios. Nos pondremos en contacto pronto.
        </p>
      </div>
    </section>

    <!-- Invitation Section -->
    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4 text-center">
        <h2 class="text-4xl font-bold mb-6">Invitación Abierta</h2>
        <p class="text-xl mb-8 text-gray-100 max-w-2xl mx-auto">
          Estamos a su disposición para coordinar una reunión, analizar su situación y proponer
          soluciones personalizadas. Nuestro compromiso es adaptarnos a cada proyecto y superar las
          expectativas con profesionalismo, innovación y calidad.
        </p>
        <p class="text-lg text-yellow-400">
          ¡Gracias por su tiempo y confianza. Quedamos a sus órdenes!
        </p>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
