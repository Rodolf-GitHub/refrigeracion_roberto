<script setup lang="ts">
import { onMounted, ref } from 'vue'

interface Proyecto {
  id: number
  nombre: string
  descripcion: string
  fecha: string
  imagen: string
}

const endpoint = 'https://api.refrigeracionroberto.com/api/proyectos/'
const proyectos = ref<Proyecto[]>([])
const loading = ref(true)
const error = ref('')

const cargarProyectos = async () => {
  try {
    loading.value = true
    error.value = ''

    const response = await fetch(endpoint)
    if (!response.ok) {
      throw new Error('No se pudieron obtener los proyectos')
    }

    const data = (await response.json()) as Proyecto[]
    proyectos.value = Array.isArray(data) ? data : []
  } catch (err) {
    console.error(err)
    error.value = 'No fue posible cargar los proyectos. Intenta nuevamente más tarde.'
    proyectos.value = []
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  cargarProyectos()
})
</script>

<template>
  <div class="w-full">
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Proyectos</h1>
        <p class="text-xl mt-4 text-gray-100">Trabajos realizados por Refrigeración Roberto</p>
      </div>
    </section>

    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <div v-if="loading" class="text-center py-10">
          <p class="text-lg text-gray-700">Cargando proyectos...</p>
        </div>

        <div v-else-if="error" class="text-center py-10 bg-white rounded-lg shadow-md">
          <p class="text-red-600 font-semibold">{{ error }}</p>
        </div>

        <div
          v-else-if="proyectos.length === 0"
          class="text-center py-10 bg-white rounded-lg shadow-md"
        >
          <p class="text-gray-700">Aún no hay proyectos publicados.</p>
        </div>

        <div v-else class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <article
            v-for="proyecto in proyectos"
            :key="proyecto.id"
            class="project-card bg-white rounded-2xl overflow-hidden"
          >
            <div class="relative h-56 overflow-hidden">
              <img
                :src="proyecto.imagen"
                :alt="proyecto.nombre"
                class="w-full h-full object-cover project-image"
              />
              <div class="absolute inset-0 project-image-overlay"></div>
              <span
                class="absolute top-3 left-3 text-xs font-bold px-3 py-1 rounded-full bg-white/90 text-blue-700"
              >
                {{ proyecto.fecha }}
              </span>
            </div>

            <div class="p-6">
              <h2 class="text-xl md:text-2xl font-bold text-blue-700 mb-3 leading-tight">
                {{ proyecto.nombre }}
              </h2>
              <p class="text-gray-700 leading-relaxed">
                {{ proyecto.descripcion }}
              </p>
            </div>
          </article>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.project-card {
  box-shadow: 0 8px 22px rgba(0, 0, 0, 0.08);
  border: 1px solid rgba(0, 119, 194, 0.08);
  transition:
    transform 0.28s ease,
    box-shadow 0.28s ease;
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 16px 30px rgba(0, 0, 0, 0.14);
}

.project-image {
  transition: transform 0.45s ease;
}

.project-card:hover .project-image {
  transform: scale(1.07);
}

.project-image-overlay {
  background: linear-gradient(to top, rgba(0, 0, 0, 0.45), rgba(0, 0, 0, 0.05));
}
</style>
