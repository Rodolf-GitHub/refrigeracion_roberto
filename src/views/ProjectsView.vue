<script setup lang="ts">
import { onMounted, ref } from 'vue'

interface Proyecto {
  id: number
  nombre: string
  descripcion: string
  fecha: string
  imagenes: string[]
}

const endpoint = 'https://api.refrigeracionroberto.com/api/proyectos/'
const proyectos = ref<Proyecto[]>([])
const loading = ref(true)
const error = ref('')

// índice activo del carrusel por proyecto
const activeIndex = ref<Record<number, number>>({})

const prev = (id: number, total: number) => {
  activeIndex.value[id] = ((activeIndex.value[id] ?? 0) - 1 + total) % total
}
const next = (id: number, total: number) => {
  activeIndex.value[id] = ((activeIndex.value[id] ?? 0) + 1) % total
}

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
    // inicializar índice en 0 para cada proyecto
    proyectos.value.forEach((p) => (activeIndex.value[p.id] = 0))
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
    <!-- Hero -->
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Proyectos</h1>
        <p class="text-xl mt-4 text-gray-100">Trabajos realizados por Refrigeración Roberto</p>
      </div>
    </section>

    <!-- Contenido -->
    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <!-- Loading -->
        <div v-if="loading" class="flex flex-col items-center py-20 gap-4">
          <div
            class="w-10 h-10 border-4 border-blue-500 border-t-transparent rounded-full animate-spin"
          ></div>
          <p class="text-gray-500">Cargando proyectos...</p>
        </div>

        <!-- Error -->
        <div v-else-if="error" class="text-center py-10 bg-white rounded-lg shadow-md">
          <p class="text-red-600 font-semibold">{{ error }}</p>
        </div>

        <!-- Sin proyectos -->
        <div
          v-else-if="proyectos.length === 0"
          class="text-center py-10 bg-white rounded-lg shadow-md"
        >
          <p class="text-gray-700">Aún no hay proyectos publicados.</p>
        </div>

        <!-- Grid de proyectos -->
        <div v-else class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <article
            v-for="proyecto in proyectos"
            :key="proyecto.id"
            class="project-card bg-white rounded-2xl overflow-hidden flex flex-col"
          >
            <!-- Carrusel de imágenes -->
            <div class="relative h-60 bg-gray-100 overflow-hidden">
              <!-- Imagen activa -->
              <template v-if="proyecto.imagenes && proyecto.imagenes.length > 0">
                <img
                  v-for="(img, idx) in proyecto.imagenes"
                  :key="idx"
                  :src="img"
                  :alt="`${proyecto.nombre} - foto ${idx + 1}`"
                  class="absolute inset-0 w-full h-full object-cover transition-opacity duration-500"
                  :class="
                    idx === (activeIndex[proyecto.id] ?? 0) ? 'opacity-100 z-10' : 'opacity-0 z-0'
                  "
                />

                <!-- Controles (solo si hay más de 1 imagen) -->
                <template v-if="proyecto.imagenes.length > 1">
                  <button
                    class="carousel-btn left-2"
                    aria-label="Imagen anterior"
                    @click.stop="prev(proyecto.id, proyecto.imagenes.length)"
                  >
                    &#8249;
                  </button>
                  <button
                    class="carousel-btn right-2"
                    aria-label="Imagen siguiente"
                    @click.stop="next(proyecto.id, proyecto.imagenes.length)"
                  >
                    &#8250;
                  </button>

                  <!-- Puntos indicadores -->
                  <div class="absolute bottom-2 left-0 right-0 flex justify-center gap-1.5 z-20">
                    <button
                      v-for="(_, idx) in proyecto.imagenes"
                      :key="idx"
                      class="dot"
                      :class="
                        idx === (activeIndex[proyecto.id] ?? 0) ? 'dot-active' : 'dot-inactive'
                      "
                      :aria-label="`Ir a imagen ${idx + 1}`"
                      @click.stop="activeIndex[proyecto.id] = idx"
                    ></button>
                  </div>
                </template>
              </template>

              <!-- Sin imágenes -->
              <div
                v-else
                class="w-full h-full flex items-center justify-center text-gray-400 text-sm"
              >
                Sin imágenes
              </div>

              <!-- Overlay + fecha -->
              <div class="absolute inset-0 project-image-overlay z-10 pointer-events-none"></div>
              <span
                class="absolute top-3 left-3 z-20 text-xs font-bold px-3 py-1 rounded-full bg-white/90 text-blue-700"
              >
                {{ proyecto.fecha }}
              </span>

              <!-- Contador de imágenes -->
              <span
                v-if="proyecto.imagenes && proyecto.imagenes.length > 1"
                class="absolute top-3 right-3 z-20 text-xs font-semibold px-2 py-1 rounded-full bg-black/50 text-white"
              >
                {{ (activeIndex[proyecto.id] ?? 0) + 1 }} / {{ proyecto.imagenes.length }}
              </span>
            </div>

            <!-- Info -->
            <div class="p-6 flex flex-col flex-1">
              <h2 class="text-xl font-bold text-blue-700 mb-2 leading-tight">
                {{ proyecto.nombre }}
              </h2>
              <p class="text-gray-600 text-sm leading-relaxed flex-1">
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

.project-image-overlay {
  background: linear-gradient(to top, rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.04));
}

.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 20;
  background: rgba(255, 255, 255, 0.85);
  color: #1d4ed8;
  border: none;
  border-radius: 9999px;
  width: 2rem;
  height: 2rem;
  font-size: 1.4rem;
  line-height: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.2s;
}

.carousel-btn:hover {
  background: #fff;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.18);
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 9999px;
  border: none;
  cursor: pointer;
  transition:
    background 0.2s,
    transform 0.2s;
}

.dot-active {
  background: #fff;
  transform: scale(1.25);
}

.dot-inactive {
  background: rgba(255, 255, 255, 0.45);
}
</style>
