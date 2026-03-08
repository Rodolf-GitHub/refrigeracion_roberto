<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, watch } from 'vue'
import { RouterLink, useRoute } from 'vue-router'
import { Phone, Mail, Users, Wrench, FolderOpen, Home, MessageCircle } from 'lucide-vue-next'

const route = useRoute()
const mobileMenuOpen = ref(false)
const installAvailable = ref(false)
let deferredPrompt: BeforeInstallPromptEvent | null = null

interface BeforeInstallPromptEvent extends Event {
  prompt: () => Promise<void>
  userChoice: Promise<{ outcome: 'accepted' | 'dismissed'; platform: string }>
}

const navLinks = [
  { to: '/', label: 'Inicio', icon: Home },
  { to: '/nosotros', label: 'Nosotros', icon: Users },
  { to: '/servicios', label: 'Servicios', icon: Wrench },
  { to: '/proyectos', label: 'Proyectos', icon: FolderOpen },
  { to: '/contacto', label: 'Contacto', icon: MessageCircle },
]

const toggleMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMenu = () => {
  mobileMenuOpen.value = false
}

// Close menu on route change
watch(() => route.path, closeMenu)

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
  <!-- Top bar desktop -->
  <div
    class="bg-blue-900 text-white py-2 px-6 md:px-10 text-xs sticky top-0 z-50 shadow-md hidden md:block"
  >
    <div class="w-full flex justify-between items-center gap-6">
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

  <!-- Main Nav -->
  <nav class="bg-gradient-to-r from-blue-700 to-blue-500 sticky top-0 md:top-0 z-50 shadow-lg">
    <div class="w-full px-6 md:px-10 py-2 md:py-3 flex justify-between items-center">
      <!-- Logo -->
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

      <div class="flex items-center gap-3">
        <!-- Install button -->
        <button
          v-if="installAvailable"
          @click="handleInstall"
          class="install-btn inline-flex items-center bg-yellow-400 text-blue-700 px-3 md:px-4 py-1.5 md:py-2 rounded-lg font-bold hover:bg-yellow-500 transition-all duration-300 shadow-md text-[11px] md:text-sm whitespace-nowrap"
        >
          Instalar aplicación
        </button>

        <!-- Hamburger button (mobile) -->
        <button
          class="md:hidden relative w-10 h-10 flex items-center justify-center rounded-lg bg-white/10 hover:bg-white/20 transition-colors duration-300"
          @click="toggleMenu"
          aria-label="Menú"
        >
          <div class="hamburger-icon" :class="{ open: mobileMenuOpen }">
            <span></span>
            <span></span>
            <span></span>
          </div>
        </button>
      </div>

      <!-- Desktop links -->
      <ul class="hidden md:flex list-none m-0 p-0 gap-1 items-center">
        <li v-for="link in navLinks" :key="link.to">
          <RouterLink
            :to="link.to"
            class="block px-5 py-3 text-white font-medium rounded-md transition-all duration-300 hover:bg-white hover:bg-opacity-10 hover:text-yellow-400 relative group"
          >
            {{ link.label }}
            <span
              class="absolute bottom-0 left-0 w-0 h-1 bg-yellow-400 rounded group-hover:w-full transition-all duration-300"
            ></span>
          </RouterLink>
        </li>
      </ul>
    </div>
  </nav>

  <!-- Mobile quick access bar -->
  <nav class="md:hidden bg-blue-700 sticky top-[56px] -mt-px z-40 shadow quick-bar">
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
    <!-- Shine line -->
    <div class="shine-line"></div>
  </nav>

  <!-- Mobile fullscreen menu -->
  <Transition name="mobile-menu">
    <div v-if="mobileMenuOpen" class="md:hidden fixed inset-0 z-[100] mobile-menu-container">
      <!-- Backdrop -->
      <div class="absolute inset-0 bg-blue-900/80 backdrop-blur-md" @click="closeMenu"></div>

      <!-- Menu panel -->
      <div class="relative h-full flex flex-col overflow-y-auto">
        <!-- Header -->
        <div class="flex items-center justify-between px-6 py-4 border-b border-white/10">
          <div class="flex items-center gap-3">
            <img src="/logo.png" alt="Refrigeración Roberto" class="h-10 w-auto" />
            <span class="text-white font-bold text-lg">Refrigeración Roberto</span>
          </div>
          <button
            @click="closeMenu"
            class="w-10 h-10 flex items-center justify-center rounded-lg bg-white/10 hover:bg-white/20 transition-colors"
            aria-label="Cerrar menú"
          >
            <div class="hamburger-icon open">
              <span></span>
              <span></span>
              <span></span>
            </div>
          </button>
        </div>

        <!-- Nav links -->
        <nav class="flex-1 px-6 py-6">
          <ul class="list-none m-0 p-0 space-y-2">
            <li
              v-for="(link, index) in navLinks"
              :key="link.to"
              class="mobile-menu-item"
              :style="{ animationDelay: `${index * 60 + 80}ms` }"
            >
              <RouterLink
                :to="link.to"
                class="mobile-nav-link"
                :class="{ 'mobile-nav-link--active': route.path === link.to }"
                @click="closeMenu"
              >
                <div class="mobile-nav-icon">
                  <component :is="link.icon" :size="22" />
                </div>
                <span class="text-base font-semibold">{{ link.label }}</span>
                <svg
                  class="ml-auto w-5 h-5 opacity-40"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M9 5l7 7-7 7"
                  />
                </svg>
              </RouterLink>
            </li>
          </ul>
        </nav>

        <!-- Contact info -->
        <div
          class="mobile-menu-item px-6 pb-6 pt-2 border-t border-white/10"
          :style="{ animationDelay: `${navLinks.length * 60 + 140}ms` }"
        >
          <p class="text-white/50 text-xs font-semibold uppercase tracking-widest mb-4">
            Contacto directo
          </p>
          <div class="space-y-3">
            <a
              href="tel:+59892698549"
              class="flex items-center gap-3 text-white/90 hover:text-yellow-400 transition-colors duration-200"
            >
              <div
                class="w-10 h-10 rounded-full bg-yellow-400/15 flex items-center justify-center flex-shrink-0"
              >
                <Phone :size="18" class="text-yellow-400" />
              </div>
              <div>
                <p class="text-sm font-semibold">+598 92 698 549</p>
                <p class="text-xs text-white/50">Llamar ahora</p>
              </div>
            </a>
            <a
              href="mailto:labradaroberto23@gmail.com"
              class="flex items-center gap-3 text-white/90 hover:text-yellow-400 transition-colors duration-200"
            >
              <div
                class="w-10 h-10 rounded-full bg-yellow-400/15 flex items-center justify-center flex-shrink-0"
              >
                <Mail :size="18" class="text-yellow-400" />
              </div>
              <div>
                <p class="text-sm font-semibold">labradaroberto23@gmail.com</p>
                <p class="text-xs text-white/50">Enviar correo</p>
              </div>
            </a>
          </div>

          <!-- Install button inside mobile menu -->
          <button
            v-if="installAvailable"
            @click="handleInstall"
            class="mt-5 w-full install-btn inline-flex items-center justify-center bg-yellow-400 text-blue-900 px-4 py-3 rounded-xl font-bold hover:bg-yellow-300 transition-all duration-300 shadow-lg text-sm"
          >
            Instalar aplicación
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
/* ── Hamburger icon ── */
.hamburger-icon {
  width: 20px;
  height: 14px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.hamburger-icon span {
  display: block;
  height: 2px;
  width: 100%;
  background: white;
  border-radius: 2px;
  transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  transform-origin: center;
}

.hamburger-icon.open span:nth-child(1) {
  transform: translateY(6px) rotate(45deg);
}

.hamburger-icon.open span:nth-child(2) {
  opacity: 0;
  transform: scaleX(0);
}

.hamburger-icon.open span:nth-child(3) {
  transform: translateY(-6px) rotate(-45deg);
}

/* ── Mobile menu transition ── */
.mobile-menu-enter-active {
  transition: opacity 0.3s ease;
}

.mobile-menu-leave-active {
  transition: opacity 0.25s ease;
}

.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
}

/* ── Staggered item reveal ── */
.mobile-menu-item {
  animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1) both;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ── Mobile nav link ── */
.mobile-nav-link {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.875rem 1rem;
  border-radius: 0.875rem;
  color: white;
  text-decoration: none;
  transition: all 0.25s ease;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid transparent;
}

.mobile-nav-link:hover,
.mobile-nav-link:active {
  background: rgba(255, 255, 255, 0.12);
  border-color: rgba(255, 255, 255, 0.1);
  transform: translateX(4px);
}

.mobile-nav-link--active {
  background: rgba(255, 210, 0, 0.12) !important;
  border-color: rgba(255, 210, 0, 0.3) !important;
}

.mobile-nav-link--active .mobile-nav-icon {
  background: rgba(255, 210, 0, 0.25);
  color: #ffd200;
}

.mobile-nav-link--active span {
  color: #ffd200;
}

/* ── Nav icon circle ── */
.mobile-nav-icon {
  width: 2.75rem;
  height: 2.75rem;
  border-radius: 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  transition: all 0.25s ease;
}

/* ── Quick access bar ── */
.mobile-link {
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  border-radius: 0.5rem;
  border: 1px solid rgba(255, 255, 255, 0.25);
  padding: 0.5rem 0.65rem;
  white-space: nowrap;
  transition: all 0.25s ease;
  background: rgba(255, 255, 255, 0.06);
}

.mobile-link:hover,
.mobile-link:active {
  background-color: rgba(255, 255, 255, 0.15);
  transform: translateY(-1px);
  border-color: rgba(255, 210, 0, 0.5);
  color: #ffd200;
}

/* ── Shine line animation ── */
.shine-line {
  height: 2px;
  width: 100%;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(255, 210, 0, 0.15) 10%,
    rgba(255, 210, 0, 0.15) 90%,
    transparent 100%
  );
  position: relative;
  overflow: hidden;
}

.shine-line::after {
  content: '';
  position: absolute;
  top: 0;
  left: -40%;
  width: 40%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 210, 0, 0.6),
    rgba(255, 255, 255, 0.9),
    rgba(255, 210, 0, 0.6),
    transparent
  );
  animation: shimmer 2.5s ease-in-out infinite;
}

@keyframes shimmer {
  0% {
    left: -40%;
  }
  100% {
    left: 100%;
  }
}

/* ── Install button pulse ── */
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
