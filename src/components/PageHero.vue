<script setup lang="ts">
defineProps<{
  badge?: string
  title: string
  subtitle?: string
}>()
</script>

<template>
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

    <div class="relative z-10 w-full px-6 md:px-10 pt-20 pb-36 text-center">
      <span
        v-if="badge"
        class="inline-block px-4 py-2 bg-[#ffd200] text-[#0b1a2b] text-sm font-bold rounded-full mb-6 shadow-lg"
      >
        {{ badge }}
      </span>
      <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-4">
        {{ title }}
      </h1>
      <p v-if="subtitle" class="text-lg md:text-xl text-[#a9c9f5] max-w-2xl mx-auto">
        {{ subtitle }}
      </p>
      <!-- Slot para contenido extra (ej: botones, búsqueda) -->
      <slot />
    </div>

    <!-- Ola divisora -->
    <div class="absolute bottom-0 left-0 right-0 leading-none z-0">
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
</template>

<style scoped>
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
</style>
