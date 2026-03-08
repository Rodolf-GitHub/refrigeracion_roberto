<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'
import { ChevronLeft, ChevronRight, Calendar, Eye, X } from 'lucide-vue-next'

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
const searchTerm = ref('')

// Por proyecto: índice de imagen activa y hover
const activeIndex = ref<Record<number, number>>({})
const hoveredId = ref<number | null>(null)

// Lightbox
const lightbox = ref<{ proyecto: Proyecto; idx: number } | null>(null)

const filteredProyectos = computed(() => {
  const q = searchTerm.value.toLowerCase()
  return proyectos.value.filter(
    (p) => p.nombre.toLowerCase().includes(q) || p.descripcion.toLowerCase().includes(q),
  )
})

function formatDate(dateStr: string) {
  const d = new Date(dateStr)
  if (isNaN(d.getTime())) return dateStr
  return d.toLocaleDateString('es-ES', { year: 'numeric', month: 'long', day: 'numeric' })
}

function prevImg(id: number, total: number) {
  activeIndex.value[id] = ((activeIndex.value[id] ?? 0) - 1 + total) % total
}
function nextImg(id: number, total: number) {
  activeIndex.value[id] = ((activeIndex.value[id] ?? 0) + 1) % total
}

function openLightbox(proyecto: Proyecto, idx: number) {
  lightbox.value = { proyecto, idx }
}
function closeLightbox() {
  lightbox.value = null
}
function lightboxPrev() {
  if (!lightbox.value) return
  const total = lightbox.value.proyecto.imagenes.length
  lightbox.value.idx = (lightbox.value.idx - 1 + total) % total
}
function lightboxNext() {
  if (!lightbox.value) return
  const total = lightbox.value.proyecto.imagenes.length
  lightbox.value.idx = (lightbox.value.idx + 1) % total
}

const cargarProyectos = async () => {
  try {
    loading.value = true
    error.value = ''
    const response = await fetch(endpoint)
    if (!response.ok) throw new Error('No se pudieron obtener los proyectos')
    const data = (await response.json()) as Proyecto[]
    proyectos.value = Array.isArray(data) ? data : []
    proyectos.value.forEach((p) => (activeIndex.value[p.id] = 0))
  } catch (err) {
    console.error(err)
    error.value = 'No fue posible cargar los proyectos. Intenta nuevamente más tarde.'
    proyectos.value = []
  } finally {
    loading.value = false
  }
}

onMounted(cargarProyectos)
</script>

<template>
  <div class="w-full min-h-screen bg-[#f4f8fc]">
    <!-- ── HEADER ─────────────────────────────── -->
    <header
      class="relative overflow-hidden"
      style="background: linear-gradient(135deg, #0d5db8 0%, #2f7ed8 50%, #0d5db8 100%)"
    >
      <!-- Blobs decorativos -->
      <div class="pointer-events-none absolute inset-0">
        <div class="blob blob-yellow" />
        <div class="blob blob-blue" />
        <div class="blob blob-white" />
      </div>

      <div class="relative w-full px-6 md:px-10 py-20 text-center">
        <span
          class="inline-block px-4 py-2 bg-[#ffd200] text-[#0b1a2b] text-sm font-bold rounded-full mb-6 shadow-lg"
        >
          Portafolio de Proyectos
        </span>
        <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-4">
          Nuestros Proyectos
        </h1>
        <p class="text-lg md:text-xl text-[#a9c9f5] max-w-2xl mx-auto mb-10">
          Descubre nuestra trayectoria a través de proyectos que transforman espacios y crean valor
          para nuestros clientes.
        </p>

        <!-- Barra de búsqueda eliminada -->
      </div>

      <!-- Ola divisora -->
      <div class="absolute bottom-0 left-0 right-0 leading-none">
        <svg
          viewBox="0 0 1440 120"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="w-full block"
          preserveAspectRatio="none"
          style="display: block; margin-bottom: -1px"
        >
          <path
            d="M0 120L60 105C120 90 240 60 360 45C480 30 600 30 720 37.5C840 45 960 60 1080 67.5C1200 75 1320 75 1380 75L1440 75V120H1380C1320 120 1200 120 1080 120C960 120 840 120 720 120C600 120 480 120 360 120C240 120 120 120 60 120H0Z"
            fill="#f4f8fc"
          />
        </svg>
      </div>
    </header>

    <!-- ── CONTENIDO ───────────────────────────── -->
    <section class="w-full px-6 md:px-10 py-12">
      <!-- Loading -->
      <div v-if="loading" class="flex flex-col items-center py-24 gap-4">
        <div
          class="w-12 h-12 border-4 border-[#0d5db8] border-t-transparent rounded-full animate-spin"
        />
        <p class="text-[#6b7a8a]">Cargando proyectos...</p>
      </div>

      <!-- Error -->
      <div v-else-if="error" class="text-center py-16 bg-white rounded-2xl shadow">
        <p class="text-red-600 font-semibold">{{ error }}</p>
      </div>

      <template v-else>
        <!-- Stats bar -->
        <div
          class="flex flex-wrap items-center justify-between gap-4 mb-10 p-5 bg-white rounded-2xl shadow-[0_4px_20px_rgba(13,93,184,0.08)]"
        >
          <div class="flex items-center gap-3">
            <div class="w-11 h-11 flex items-center justify-center bg-[#a9c9f5]/30 rounded-xl">
              <svg
                class="w-6 h-6 text-[#0d5db8]"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
                />
              </svg>
            </div>
            <div>
              <p class="text-2xl font-bold text-[#0b1a2b]">{{ filteredProyectos.length }}</p>
              <p class="text-sm text-[#6b7a8a]">Proyectos encontrados</p>
            </div>
          </div>
        </div>

        <!-- Sin resultados -->
        <div v-if="filteredProyectos.length === 0" class="text-center py-20">
          <div
            class="w-24 h-24 mx-auto mb-6 bg-[#e6eef7] rounded-full flex items-center justify-center"
          >
            <svg
              class="w-12 h-12 text-[#6b7a8a]"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9.172 16.172a4 4 0 015.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
              />
            </svg>
          </div>
          <h3 class="text-xl font-semibold text-[#0b1a2b] mb-2">No se encontraron proyectos</h3>
          <p class="text-[#6b7a8a]">Intenta con otros términos de búsqueda</p>
        </div>

        <!-- Grid de proyectos -->
        <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <article
            v-for="proyecto in filteredProyectos"
            :key="proyecto.id"
            class="project-card group"
            @mouseenter="hoveredId = proyecto.id"
            @mouseleave="hoveredId = null"
          >
            <!-- ── Sección imagen ── -->
            <div class="relative h-72 overflow-hidden bg-[#e6eef7]">
              <!-- Imagen principal -->
              <template v-if="proyecto.imagenes && proyecto.imagenes.length > 0">
                <img
                  :src="proyecto.imagenes[activeIndex[proyecto.id] ?? 0]"
                  :alt="`${proyecto.nombre} - Imagen ${(activeIndex[proyecto.id] ?? 0) + 1}`"
                  class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105"
                />

                <!-- Overlay -->
                <div
                  class="absolute inset-0 bg-gradient-to-t from-[#0b1a2b]/60 via-transparent to-transparent pointer-events-none"
                />

                <!-- Contador -->
                <div
                  class="absolute top-4 right-4 flex items-center gap-1.5 bg-white/95 backdrop-blur-sm px-3 py-1.5 rounded-full shadow-lg z-10"
                >
                  <Eye class="w-4 h-4 text-[#0d5db8]" />
                  <span class="text-sm font-medium text-[#0b1a2b]">
                    {{ (activeIndex[proyecto.id] ?? 0) + 1 }}/{{ proyecto.imagenes.length }}
                  </span>
                </div>

                <!-- Flechas (visibles al hover, CSS puro) -->
                <template v-if="proyecto.imagenes.length > 1">
                  <button
                    class="carousel-arrow carousel-arrow-left"
                    aria-label="Imagen anterior"
                    @click.stop="prevImg(proyecto.id, proyecto.imagenes.length)"
                  >
                    <ChevronLeft class="w-5 h-5" />
                  </button>
                  <button
                    class="carousel-arrow carousel-arrow-right"
                    aria-label="Siguiente imagen"
                    @click.stop="nextImg(proyecto.id, proyecto.imagenes.length)"
                  >
                    <ChevronRight class="w-5 h-5" />
                  </button>

                  <!-- Dots -->
                  <div class="absolute bottom-4 left-1/2 -translate-x-1/2 flex gap-2 z-10">
                    <button
                      v-for="(_, i) in proyecto.imagenes"
                      :key="i"
                      class="dot"
                      :class="i === (activeIndex[proyecto.id] ?? 0) ? 'dot-active' : 'dot-inactive'"
                      :aria-label="`Ir a imagen ${i + 1}`"
                      @click.stop="activeIndex[proyecto.id] = i"
                    />
                  </div>
                </template>
              </template>

              <!-- Sin imágenes -->
              <div
                v-else
                class="w-full h-full flex flex-col items-center justify-center gap-2 text-[#94a3b8] text-sm"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="w-10 h-10"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="1.5"
                    d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
                  />
                </svg>
                Sin imágenes
              </div>

              <!-- Acento de esquina (hover) -->
              <div class="absolute top-0 left-0 w-20 h-20 overflow-hidden pointer-events-none">
                <div
                  class="absolute -top-10 -left-10 w-20 h-20 bg-[#ffd200] rotate-45 opacity-0 group-hover:opacity-100 transition-opacity duration-500"
                />
              </div>
            </div>

            <!-- Thumbnails -->
            <div
              v-if="proyecto.imagenes && proyecto.imagenes.length > 1"
              class="flex gap-2 px-4 py-3 bg-[#f4f8fc] border-b border-[#e6eef7] overflow-x-auto"
            >
              <button
                v-for="(img, idx) in proyecto.imagenes"
                :key="idx"
                class="thumbnail"
                :class="
                  (activeIndex[proyecto.id] ?? 0) === idx
                    ? 'thumbnail-active'
                    : 'thumbnail-inactive'
                "
                @click="openLightbox(proyecto, idx)"
              >
                <img :src="img" :alt="`Miniatura ${idx + 1}`" class="w-full h-full object-cover" />
              </button>
            </div>

            <!-- ── Cuerpo ── -->
            <div class="p-6 flex flex-col flex-1">
              <!-- Badge fecha -->
              <div class="flex items-center gap-2 mb-3">
                <span
                  class="inline-flex items-center gap-1.5 px-3 py-1 bg-[#fff2b3] text-[#c9a400] text-xs font-semibold rounded-full"
                >
                  <Calendar class="w-3.5 h-3.5" />
                  {{ formatDate(proyecto.fecha) }}
                </span>
              </div>

              <!-- Título -->
              <h2
                class="text-xl font-bold text-[#0b1a2b] mb-3 group-hover:text-[#0d5db8] transition-colors duration-300"
              >
                {{ proyecto.nombre }}
              </h2>

              <!-- Descripción -->
              <p class="text-[#3b4a5a] text-sm leading-relaxed card-desc flex-1 mb-5">
                {{ proyecto.descripcion }}
              </p>

              <!-- Botón -->
              <button class="btn-ver">Ver Proyecto Completo</button>
            </div>
          </article>
        </div>
      </template>
    </section>

    <!-- ── FOOTER CTA ──────────────────────────── -->
    <section class="mt-8" style="background: linear-gradient(90deg, #0b1a2b 0%, #0d5db8 100%)">
      <div class="w-full px-6 md:px-10 py-16 text-center">
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-4">
          ¿Tenés un equipo para reparar?
        </h2>
        <p class="text-[#a9c9f5] mb-8 text-lg">Contactanos y te damos solución rápida</p>
        <a
          href="/contacto"
          class="inline-block px-8 py-4 bg-[#ffd200] text-[#0b1a2b] font-bold rounded-xl hover:bg-[#c9a400] transition-all duration-300 hover:scale-105 shadow-lg"
        >
          Solicitar Presupuesto
        </a>
      </div>
    </section>

    <!-- ── LIGHTBOX ────────────────────────────── -->
    <Teleport to="body">
      <div v-if="lightbox" class="lightbox-overlay" @click="closeLightbox">
        <!-- Cerrar -->
        <button class="lightbox-btn top-6 right-6" aria-label="Cerrar" @click="closeLightbox">
          <X class="w-6 h-6" />
        </button>

        <!-- Flecha izq -->
        <button
          class="lightbox-btn left-6 top-1/2 -translate-y-1/2"
          aria-label="Anterior"
          @click.stop="lightboxPrev"
        >
          <ChevronLeft class="w-7 h-7" />
        </button>

        <!-- Imagen -->
        <div class="max-w-5xl max-h-[80vh] mx-4 z-10" @click.stop>
          <img
            :src="lightbox.proyecto.imagenes[lightbox.idx]"
            :alt="`${lightbox.proyecto.nombre} - Imagen ${lightbox.idx + 1}`"
            class="max-w-full max-h-[78vh] object-contain rounded-2xl shadow-2xl"
          />
          <p class="text-center text-white/70 text-sm mt-4">
            {{ lightbox.idx + 1 }} de {{ lightbox.proyecto.imagenes.length }} —
            {{ lightbox.proyecto.nombre }}
          </p>
        </div>

        <!-- Flecha der -->
        <button
          class="lightbox-btn right-6 top-1/2 -translate-y-1/2"
          aria-label="Siguiente"
          @click.stop="lightboxNext"
        >
          <ChevronRight class="w-7 h-7" />
        </button>

        <!-- Thumbnails lightbox -->
        <div class="absolute bottom-6 left-1/2 -translate-x-1/2 flex gap-3 z-10" @click.stop>
          <button
            v-for="(img, idx) in lightbox.proyecto.imagenes"
            :key="idx"
            class="lightbox-thumb"
            :class="lightbox.idx === idx ? 'lightbox-thumb-active' : 'lightbox-thumb-inactive'"
            @click.stop="lightbox!.idx = idx"
          >
            <img :src="img" :alt="`Miniatura ${idx + 1}`" class="w-full h-full object-cover" />
          </button>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<style scoped>
/* ── Blobs decorativos del header ─────────── */
.blob {
  position: absolute;
  border-radius: 9999px;
  filter: blur(60px);
}
.blob-yellow {
  top: 0;
  right: 0;
  width: 24rem;
  height: 24rem;
  background: rgba(255, 210, 0, 0.12);
  transform: translate(50%, -50%);
}
.blob-blue {
  bottom: 0;
  left: 0;
  width: 20rem;
  height: 20rem;
  background: rgba(169, 201, 245, 0.2);
  transform: translate(-50%, 50%);
}
.blob-white {
  top: 50%;
  left: 50%;
  width: 16rem;
  height: 16rem;
  background: rgba(255, 255, 255, 0.06);
  transform: translate(-50%, -50%);
}

/* ── Card ─────────────────────────────────── */
.project-card {
  position: relative;
  background: #ffffff;
  border-radius: 1rem;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 20px rgba(13, 93, 184, 0.08);
  transition:
    transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1),
    box-shadow 0.4s ease;
}
.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 40px rgba(13, 93, 184, 0.15);
}

/* ── Flechas del carrusel ─────────────────── */
.carousel-arrow {
  position: absolute;
  top: 50%;
  z-index: 20;
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(4px);
  border-radius: 9999px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.18);
  color: #0d5db8;
  border: none;
  cursor: pointer;
  opacity: 0;
  transition:
    background 0.25s,
    color 0.25s,
    opacity 0.3s,
    transform 0.3s;
}
.carousel-arrow-left {
  left: 0.75rem;
  transform: translateY(-50%) translateX(-0.5rem);
}
.carousel-arrow-right {
  right: 0.75rem;
  transform: translateY(-50%) translateX(0.5rem);
}
.project-card:hover .carousel-arrow {
  opacity: 1;
}
.project-card:hover .carousel-arrow-left {
  transform: translateY(-50%) translateX(0);
}
.project-card:hover .carousel-arrow-right {
  transform: translateY(-50%) translateX(0);
}
.carousel-arrow:hover {
  background: #0d5db8;
  color: #fff;
}
/* En móvil siempre visibles (sin hover) */
@media (max-width: 767px) {
  .carousel-arrow {
    opacity: 1;
  }
  .carousel-arrow-left {
    transform: translateY(-50%) translateX(0);
  }
  .carousel-arrow-right {
    transform: translateY(-50%) translateX(0);
  }
}

/* ── Dots ─────────────────────────────────── */
.dot {
  border: none;
  cursor: pointer;
  border-radius: 9999px;
  height: 0.5rem;
  transition: all 0.3s;
}
.dot-active {
  width: 1.5rem;
  background: #ffd200;
}
.dot-inactive {
  width: 0.5rem;
  background: rgba(255, 255, 255, 0.6);
}
.dot-inactive:hover {
  background: #fff;
}

/* ── Thumbnails ───────────────────────────── */
.thumbnail {
  flex-shrink: 0;
  width: 3.5rem;
  height: 2.5rem;
  border-radius: 0.5rem;
  overflow: hidden;
  border: none;
  cursor: pointer;
  transition: all 0.25s;
}
.thumbnail-active {
  outline: 2px solid #0d5db8;
  outline-offset: 2px;
}
.thumbnail-inactive {
  opacity: 0.65;
}
.thumbnail-inactive:hover {
  opacity: 1;
}

/* ── Botón ver proyecto ───────────────────── */
.btn-ver {
  width: 100%;
  padding: 0.75rem 1.25rem;
  background: linear-gradient(90deg, #0d5db8 0%, #2f7ed8 100%);
  color: #fff;
  font-weight: 700;
  font-size: 0.9rem;
  border-radius: 0.75rem;
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(13, 93, 184, 0.3);
  transition: all 0.3s;
}
.btn-ver:hover {
  background: linear-gradient(90deg, #2f7ed8 0%, #0d5db8 100%);
  transform: scale(1.02);
}
.btn-ver:active {
  transform: scale(0.98);
}

/* ── Card desc clamp ──────────────────────── */
.card-desc {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* ── Lightbox ─────────────────────────────── */
.lightbox-overlay {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(11, 26, 43, 0.95);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
}
.lightbox-btn {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 3rem;
  height: 3rem;
  background: rgba(255, 255, 255, 0.1);
  border: none;
  border-radius: 9999px;
  color: #fff;
  cursor: pointer;
  z-index: 20;
  transition: background 0.25s;
}
.lightbox-btn:hover {
  background: #0d5db8;
}
.lightbox-thumb {
  flex-shrink: 0;
  width: 4rem;
  height: 3rem;
  border-radius: 0.5rem;
  overflow: hidden;
  border: none;
  cursor: pointer;
  transition: all 0.25s;
}
.lightbox-thumb-active {
  outline: 2px solid #ffd200;
  outline-offset: 2px;
  transform: scale(1.1);
}
.lightbox-thumb-inactive {
  opacity: 0.55;
}
.lightbox-thumb-inactive:hover {
  opacity: 1;
}
</style>
