<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const selectedImage = ref<string | null>(null)
const selectedImageIndex = ref(0)
const currentProjectIndex = ref(0)

const projects = ref([
  {
    name: 'Edificio RIBA',
    year: 2024,
    description: 'Instalación eléctrica en edificio RIBA',
    images: [
      '/edificio RIBA/Photos-001/IMG_20241008_144836.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_144852.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_145234.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_145246.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_145502.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_145512.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_145520.jpg',
      '/edificio RIBA/Photos-001/IMG_20241008_145527.jpg',
      '/edificio RIBA/Photos-0041/IMG_20241112_111250.jpg',
      '/edificio RIBA/Photos-0041/IMG_20241112_111259.jpg',
      '/edificio RIBA/Photos-0041/IMG_20241112_111504.jpg',
      '/edificio RIBA/Photos-0041/IMG_20241112_111603.jpg',
      '/edificio RIBA/Photos-0041/IMG_20241112_111658.jpg',
      '/edificio RIBA/Photos-0201/IMG_20241107_144403.jpg',
      '/edificio RIBA/Photos-0201/IMG_20241107_144417.jpg',
      '/edificio RIBA/Photos-0201/IMG_20241107_144520.jpg',
      '/edificio RIBA/Photos-0201/IMG_20241107_144523.jpg',
      '/edificio RIBA/Photos-0201/IMG_20241107_144528.jpg',
      '/edificio RIBA/Photos-0201/IMG_20241107_144533.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_070838.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_070850.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_070903.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_070912.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_070920.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_071014.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_071019.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_071023.jpg',
      '/edificio RIBA/Photos-0301/IMG_20241116_071101.jpg',
    ],
  },
  {
    name: 'Obra Sebamar',
    year: 2024,
    description: 'Instalación eléctrica en oficinas Sebamar',
    images: [
      '/Obra Sebamar/IMG-20240910-WA0034.jpg',
      '/Obra Sebamar/IMG-20240910-WA0035.jpg',
      '/Obra Sebamar/IMG-20240910-WA0036.jpg',
      '/Obra Sebamar/IMG-20240910-WA0037.jpg',
      '/Obra Sebamar/IMG-20240910-WA0038.jpg',
    ],
  },
  {
    name: 'Oficina Comunal Z10',
    year: 2024,
    description: 'Instalación eléctrica y cámaras de seguridad',
    images: [
      '/Oficina comunal 10/IMG-20240911-WA0006.jpg',
      '/Oficina comunal 10/IMG-20240911-WA0009.jpg',
      '/Oficina comunal 10/IMG-20240911-WA0010.jpg',
    ],
  },
  {
    name: 'Oficinas de Nueva Helvecia',
    year: 2024,
    description: 'Instalación eléctrica en oficinas',
    images: [
      '/Oficinas de Nueva Helvecia/IMG-20231120-WA0040.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240704-WA0025.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240704-WA0026.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240822-WA0029.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240822-WA0031.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240910-WA0040.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240910-WA0041.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240911-WA0003.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240911-WA0004.jpg',
      '/Oficinas de Nueva Helvecia/IMG-20240911-WA0005.jpg',
    ],
  },
  {
    name: 'Puerto TCP Stiler',
    year: 2024,
    description: 'Obrador para ampliación y dragado de terminal portuaria',
    images: [
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112225.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112234.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112255.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112300.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112416.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112424.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_112431.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_174706.jpg',
      '/Puerto TCP Stiler/Photos-001 (3)/IMG_20240531_174711.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240419_114813.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240419_114826.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240419_114829.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240419_114834.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240426_103442.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240426_103453.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240426_103554.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240426_103559.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240426_103612.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240426_103629.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240429_071114.jpg',
      '/Puerto TCP Stiler/Photos-00ZD1 (3)/IMG_20240429_071132.jpg',
    ],
  },
  {
    name: 'Rehabilitación de Axion',
    year: 2025,
    description: 'Rehabilitación de instalación eléctrica en oficinas y locales comerciales',
    images: [
      '/Reabilitacion de Axion/1758998262327.jpg',
      '/Reabilitacion de Axion/1758998262385.jpg',
      '/Reabilitacion de Axion/1758998262451.jpg',
      '/Reabilitacion de Axion/IMG-20231110-WA0000.jpg',
      '/Reabilitacion de Axion/IMG-20231120-WA0039.jpg',
      '/Reabilitacion de Axion/IMG-20240816-WA0002.jpg',
      '/Reabilitacion de Axion/IMG-20240816-WA0004.jpg',
      '/Reabilitacion de Axion/IMG-20240816-WA0005.jpg',
      '/Reabilitacion de Axion/IMG-20240920-WA0033.jpg',
      '/Reabilitacion de Axion/IMG-20240920-WA0034.jpg',
    ],
  },
  {
    name: 'UCUDAL SAN JOSE',
    year: 2023,
    description: 'Instalación eléctrica de potencia para nueva sede',
    images: [
      '/UCUDAL SAN JOSE/IMG_20250318_181223.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181226.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181232.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181244.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181248.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181322.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181336.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181346.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181357.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181417.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181424.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181454.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181500.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181509.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181515.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181535.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181548.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181628.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181647.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181704.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181710.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181724.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181826.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181840.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181859.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181933.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_181955.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182009.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182021.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182038.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182136.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182150.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182156.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182202.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182214.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182219.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182235.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182239.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182251.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182343.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182353.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182355.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182357.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182401.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182419.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182439.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182444.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182448.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182513.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182550.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182607.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182611.jpg',
      '/UCUDAL SAN JOSE/IMG_20250318_182657.jpg',
    ],
  },
  {
    name: 'Vivienda Salmain Jardines de Carrasco',
    year: 2025,
    description: 'Instalación eléctrica en viviendas',
    images: [
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094301.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094331.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094347.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094352.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094358.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094401.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-001 (3)/IMG_20241126_094407.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-00DSF1 (3)/IMG_20241119_103801.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-00DSF1 (3)/IMG_20241119_103807.jpg',
      '/Vivienda Salmain Jardines de Carrasco/Photos-00DSF1 (3)/IMG_20241119_104306.jpg',
    ],
  },
])

const openFullscreen = (image: string, projectIdx: number, imgIdx: number) => {
  selectedImage.value = image
  currentProjectIndex.value = projectIdx
  selectedImageIndex.value = imgIdx
}

const closeFullscreen = () => {
  selectedImage.value = null
}

const goToPrevious = () => {
  const currentProject = projects.value[currentProjectIndex.value]
  if (currentProject && selectedImageIndex.value > 0) {
    selectedImageIndex.value--
    selectedImage.value = currentProject.images[selectedImageIndex.value] || null
  }
}

const goToNext = () => {
  const currentProject = projects.value[currentProjectIndex.value]
  if (currentProject && selectedImageIndex.value < currentProject.images.length - 1) {
    selectedImageIndex.value++
    selectedImage.value = currentProject.images[selectedImageIndex.value] || null
  }
}

const handleKeydown = (e: KeyboardEvent) => {
  if (!selectedImage.value) return
  if (e.key === 'Escape') {
    closeFullscreen()
  } else if (e.key === 'ArrowLeft') {
    goToPrevious()
  } else if (e.key === 'ArrowRight') {
    goToNext()
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <div class="w-full">
    <!-- Hero Section -->
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Nuestros Proyectos</h1>
        <p class="text-xl mt-4 text-gray-100">Experiencia comprobada en el mercado</p>
      </div>
    </section>

    <!-- Projects Grid -->
    <section class="py-16 bg-white">
      <div class="max-w-6xl mx-auto px-4">
        <div class="grid gap-8">
          <div
            v-for="(project, index) in projects"
            :key="index"
            class="bg-white rounded-lg shadow-lg overflow-hidden border-t-4 border-yellow-400 hover:shadow-xl transition-shadow"
          >
            <!-- Project Header -->
            <div class="bg-gradient-to-r from-blue-700 to-blue-600 text-white p-6">
              <h2 class="text-3xl font-bold">{{ project.name }}</h2>
              <p class="text-blue-100 mt-2">{{ project.description }}</p>
              <div
                class="mt-3 inline-block bg-blue-500 px-3 py-1 rounded-full text-sm font-semibold"
              >
                Año {{ project.year }}
              </div>
            </div>

            <!-- Project Gallery -->
            <div class="p-6">
              <p class="text-sm font-semibold text-gray-700 mb-4">
                {{ project.images.length }} imágenes del proyecto
              </p>
              <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
                <button
                  v-for="(image, imgIndex) in project.images"
                  :key="imgIndex"
                  @click="openFullscreen(image, index, imgIndex)"
                  class="relative overflow-hidden rounded-lg group"
                >
                  <img
                    :src="image"
                    :alt="project.name"
                    class="w-full h-40 object-cover group-hover:scale-110 transition-transform duration-300 cursor-pointer"
                  />
                  <div
                    class="absolute inset-0 bg-black/50 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center"
                  >
                    <span class="text-white text-2xl">🔍</span>
                  </div>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Call to Action -->
    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4 text-center">
        <h2 class="text-4xl font-bold mb-6">¿Tu proyecto es el siguiente?</h2>
        <p class="text-xl mb-8 text-gray-100">
          Nos encantaría trabajar con vos. Contacta con nosotros para una consulta gratuita.
        </p>
        <RouterLink
          to="/contacto#formulario"
          class="inline-block bg-yellow-400 text-blue-700 px-10 py-4 rounded-lg font-bold hover:bg-yellow-500 transition-all duration-300 hover:shadow-lg text-lg"
        >
          Solicitar Información
        </RouterLink>
      </div>
    </section>

    <!-- Fullscreen Image Modal -->
    <div
      v-if="selectedImage"
      @click="closeFullscreen"
      class="fixed inset-0 bg-black/90 z-50 flex items-center justify-center p-4"
    >
      <button
        @click.stop="closeFullscreen"
        class="absolute top-4 right-4 text-white hover:text-gray-300 text-3xl z-60"
        aria-label="Cerrar"
      >
        ✕
      </button>

      <!-- Image Container -->
      <div
        @click.stop
        class="relative max-w-4xl max-h-[90vh] w-full h-full flex items-center justify-center"
      >
        <img
          v-if="selectedImage && projects[currentProjectIndex]"
          :src="selectedImage"
          :alt="projects[currentProjectIndex]?.name"
          class="max-w-full max-h-full object-contain"
        />

        <!-- Counter -->
        <div
          v-if="projects[currentProjectIndex]"
          class="absolute bottom-4 left-4 bg-black/50 text-white px-4 py-2 rounded-lg text-sm"
        >
          {{ selectedImageIndex + 1 }} / {{ projects[currentProjectIndex]?.images.length }}
        </div>

        <!-- Navigation Arrows -->
        <button
          v-if="selectedImageIndex > 0"
          @click.stop="goToPrevious"
          class="absolute left-4 top-1/2 transform -translate-y-1/2 bg-white/20 hover:bg-white/40 text-white p-3 rounded-full transition-all"
          aria-label="Imagen anterior"
        >
          ❮
        </button>
        <button
          v-if="
            projects[currentProjectIndex] &&
            selectedImageIndex < projects[currentProjectIndex]!.images.length - 1
          "
          @click.stop="goToNext"
          class="absolute right-4 top-1/2 transform -translate-y-1/2 bg-white/20 hover:bg-white/40 text-white p-3 rounded-full transition-all"
          aria-label="Siguiente imagen"
        >
          ❯
        </button>
      </div>

      <!-- Instructions -->
      <div class="absolute bottom-4 right-4 text-white/70 text-sm text-right">
        <p>Flechas: Anterior/Siguiente</p>
        <p>ESC: Cerrar</p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
