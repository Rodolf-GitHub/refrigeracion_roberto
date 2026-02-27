<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { RouterLink } from 'vue-router'
import { Phone, Mail, Users, Wrench, FolderOpen } from 'lucide-vue-next'

const installAvailable = ref(false)
let deferredPrompt: BeforeInstallPromptEvent | null = null

interface BeforeInstallPromptEvent extends Event {
  prompt: () => Promise<void>
  userChoice: Promise<{ outcome: 'accepted' | 'dismissed'; platform: string }>
}

const onBeforeInstallPrompt = (event: Event) => {
  event.preventDefault()
  deferredPrompt = event as BeforeInstallPromptEvent
  installAvailable.value = true
}

const handleInstall = async () => {
  if (!deferredPrompt) return

  await deferredPrompt.prompt()
  await deferredPrompt.userChoice
  deferredPrompt = null
  installAvailable.value = false
}

onMounted(() => {
  window.addEventListener('beforeinstallprompt', onBeforeInstallPrompt)
})

onBeforeUnmount(() => {
  window.removeEventListener('beforeinstallprompt', onBeforeInstallPrompt)
})
</script>

<template>
  <div class="bg-blue-900 text-white py-2 px-4 text-xs sticky top-0 z-50 shadow-md hidden md:block">
    <div class="max-w-6xl mx-auto flex justify-between items-center gap-6">
      <div class="flex gap-8">
        <div class="flex items-center gap-2">
          <Phone :size="14" class="text-yellow-400" />
          <a href="tel:+59892698549" class="text-yellow-400 font-bold hover:underline"
            >+598 92 698 549</a
          >
        </div>
      </div>
      <div class="flex items-center gap-2">
        <Mail :size="14" class="text-yellow-400" />
        <a
          href="mailto:labradaroberto23@gmail.com"
          class="text-yellow-400 font-bold hover:underline"
          >labradaroberto23@gmail.com</a
        >
      </div>
    </div>
  </div>

  <nav class="bg-gradient-to-r from-blue-700 to-blue-500 sticky top-0 md:top-0 z-50 shadow-lg">
    <div class="max-w-6xl mx-auto px-3 md:px-4 py-2 md:py-3 flex justify-between items-center">
      <div class="flex items-center gap-2 md:gap-3 min-w-0">
        <RouterLink to="/" class="hover:scale-105 transition-transform duration-300">
          <img src="/logo.png" alt="Refrigeración Roberto" class="h-10 md:h-16 w-auto" />
        </RouterLink>
        <RouterLink
          to="/"
          class="bg-white/95 rounded-lg px-2.5 md:px-4 py-1.5 md:py-2 hover:shadow-lg hover:translate-y-[-2px] transition-all duration-300"
        >
          <div class="text-sm leading-tight">
            <p class="text-blue-700 font-bold text-sm md:text-lg">Refrigeración Roberto</p>
            <p class="hidden md:block text-yellow-500 font-semibold text-xs tracking-wider">
              Mantenimiento y Reparación
            </p>
          </div>
        </RouterLink>
      </div>

      <div class="flex items-center gap-2">
        <button
          v-if="installAvailable"
          @click="handleInstall"
          class="install-btn inline-flex items-center bg-yellow-400 text-blue-700 px-3 md:px-4 py-1.5 md:py-2 rounded-lg font-bold hover:bg-yellow-500 transition-all duration-300 shadow-md text-[11px] md:text-sm whitespace-nowrap"
        >
          Instalar aplicación
        </button>
      </div>

      <ul class="hidden md:flex list-none m-0 p-0 gap-1 items-center">
        <li>
          <RouterLink
            to="/"
            class="block px-5 py-3 text-white font-medium rounded-md transition-all duration-300 hover:bg-white hover:bg-opacity-10 hover:text-yellow-400 relative group"
          >
            Inicio
            <span
              class="absolute bottom-0 left-0 w-0 h-1 bg-yellow-400 rounded group-hover:w-full transition-all duration-300"
            ></span>
          </RouterLink>
        </li>
        <li>
          <RouterLink
            to="/nosotros"
            class="block px-5 py-3 text-white font-medium rounded-md transition-all duration-300 hover:bg-white hover:bg-opacity-10 hover:text-yellow-400 relative group"
          >
            Nosotros
            <span
              class="absolute bottom-0 left-0 w-0 h-1 bg-yellow-400 rounded group-hover:w-full transition-all duration-300"
            ></span>
          </RouterLink>
        </li>
        <li>
          <RouterLink
            to="/servicios"
            class="block px-5 py-3 text-white font-medium rounded-md transition-all duration-300 hover:bg-white hover:bg-opacity-10 hover:text-yellow-400 relative group"
          >
            Servicios
            <span
              class="absolute bottom-0 left-0 w-0 h-1 bg-yellow-400 rounded group-hover:w-full transition-all duration-300"
            ></span>
          </RouterLink>
        </li>
        <li>
          <RouterLink
            to="/proyectos"
            class="block px-5 py-3 text-white font-medium rounded-md transition-all duration-300 hover:bg-white hover:bg-opacity-10 hover:text-yellow-400 relative group"
          >
            Proyectos
            <span
              class="absolute bottom-0 left-0 w-0 h-1 bg-yellow-400 rounded group-hover:w-full transition-all duration-300"
            ></span>
          </RouterLink>
        </li>
        <li>
          <RouterLink
            to="/contacto"
            class="block px-5 py-3 text-white font-medium rounded-md transition-all duration-300 hover:bg-white hover:bg-opacity-10 hover:text-yellow-400 relative group"
          >
            Contacto
            <span
              class="absolute bottom-0 left-0 w-0 h-1 bg-yellow-400 rounded group-hover:w-full transition-all duration-300"
            ></span>
          </RouterLink>
        </li>
      </ul>
    </div>
  </nav>

  <nav class="md:hidden bg-blue-700 border-t border-blue-500 sticky top-[56px] -mt-px z-40 shadow">
    <div class="px-2 py-2 flex items-center justify-between gap-1 overflow-x-auto">
      <RouterLink to="/nosotros" class="mobile-link">
        <Users :size="16" />
        <span>Nosotros</span>
      </RouterLink>
      <RouterLink to="/servicios" class="mobile-link">
        <Wrench :size="16" />
        <span>Servicios</span>
      </RouterLink>
      <RouterLink to="/proyectos" class="mobile-link">
        <FolderOpen :size="16" />
        <span>Proyectos</span>
      </RouterLink>
      <RouterLink to="/contacto" class="mobile-link">
        <Phone :size="16" />
        <span>Contacto</span>
      </RouterLink>
    </div>
  </nav>
</template>

<style scoped>
.mobile-link {
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  border-radius: 0.5rem;
  border: 1px solid rgba(255, 255, 255, 0.35);
  padding: 0.5rem 0.55rem;
  white-space: nowrap;
  transition:
    background-color 0.25s ease,
    transform 0.25s ease;
}

.mobile-link:hover {
  background-color: rgba(255, 255, 255, 0.12);
  transform: translateY(-1px);
}

.install-btn {
  animation: softPulse 1.8s ease-in-out infinite;
}

@keyframes softPulse {
  0% {
    transform: translateY(0);
    box-shadow: 0 6px 14px rgba(0, 0, 0, 0.2);
  }
  50% {
    transform: translateY(-1px);
    box-shadow: 0 8px 18px rgba(0, 0, 0, 0.28);
  }
  100% {
    transform: translateY(0);
    box-shadow: 0 6px 14px rgba(0, 0, 0, 0.2);
  }
}
</style>
