<script setup lang="ts">
import { Award, Users, Lightbulb, Shield } from 'lucide-vue-next'
</script>

<template>
  <div class="w-full">
    <!-- Hero Section -->
    <section class="bg-gradient-to-r from-blue-700 to-blue-500 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl md:text-5xl font-bold">Sobre TecnoRaíz</h1>
        <p class="text-xl mt-4 text-gray-100">Ingeniería, innovación y compromiso sostenible</p>
      </div>
    </section>

    <!-- History Section -->
    <section class="py-16 bg-white">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-8">Nuestra Historia</h2>
        <div class="bg-blue-50 p-8 rounded-lg border-l-4 border-yellow-400">
          <p class="text-gray-700 text-lg leading-relaxed mb-4">
            Tecno Raíz es un emprendimiento joven con raíces firmes en la ingeniería eléctrica.
            Aunque recién comenzamos a operar como empresa, nuestros cimientos están construidos
            sobre <strong>más de cinco años de experiencia profesional</strong> en el rubro.
          </p>
          <p class="text-gray-700 text-lg leading-relaxed">
            Fundada por los ingenieros <strong>Liesvy Delgado</strong> y
            <strong>Richard Cruz</strong>, Tecno Raíz nace con el propósito de ofrecer soluciones
            eléctricas modernas, seguras y eficientes, combinando conocimiento técnico con
            compromiso ambiental.
          </p>
        </div>
      </div>
    </section>

    <!-- Founders Section -->
    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-12 text-center">Nuestros Fundadores</h2>
        <div class="grid md:grid-cols-2 gap-8">
          <div class="bg-white rounded-lg shadow-md p-8">
            <div class="flex items-center gap-4 mb-6">
              <div class="w-16 h-16 bg-yellow-400 rounded-full flex items-center justify-center">
                <Users :size="32" class="text-blue-700" />
              </div>
              <div>
                <h3 class="text-2xl font-bold text-blue-700">Ing. Liesvy Delgado</h3>
                <p class="text-yellow-400 font-semibold">+598 094840059</p>
              </div>
            </div>
            <p class="text-gray-700 leading-relaxed">
              Ingeniero eléctrico con más de 5 años de trayectoria en diseño, ejecución y
              supervisión de instalaciones eléctricas complejas. Ha liderado proyectos en industrias
              de manufactura, edificios corporativos e infraestructura pública.
            </p>
          </div>
          <div class="bg-white rounded-lg shadow-md p-8">
            <div class="flex items-center gap-4 mb-6">
              <div class="w-16 h-16 bg-yellow-400 rounded-full flex items-center justify-center">
                <Users :size="32" class="text-blue-700" />
              </div>
              <div>
                <h3 class="text-2xl font-bold text-blue-700">Ing. Richard Cruz</h3>
                <p class="text-yellow-400 font-semibold">+598 094774616</p>
              </div>
            </div>
            <p class="text-gray-700 leading-relaxed">
              Ingeniero eléctrico especializado en instalaciones de potencia y sistemas de control.
              Con experiencia demostrada en proyectos residenciales, comerciales e industriales de
              envergadura.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Values Section -->
    <section class="py-16 bg-white">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-12 text-center">Nuestros Valores</h2>
        <div class="grid md:grid-cols-4 gap-6">
          <div class="text-center">
            <Award :size="48" class="text-yellow-400 mx-auto mb-4" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Excelencia</h3>
            <p class="text-gray-700">Compromiso con la calidad en cada proyecto</p>
          </div>
          <div class="text-center">
            <Shield :size="48" class="text-yellow-400 mx-auto mb-4" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Seguridad</h3>
            <p class="text-gray-700">Máximos estándares en protección laboral</p>
          </div>
          <div class="text-center">
            <Lightbulb :size="48" class="text-yellow-400 mx-auto mb-4" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Innovación</h3>
            <p class="text-gray-700">Tecnologías modernas y sostenibles</p>
          </div>
          <div class="text-center">
            <Users :size="48" class="text-yellow-400 mx-auto mb-4" />
            <h3 class="text-xl font-bold text-blue-700 mb-2">Profesionalismo</h3>
            <p class="text-gray-700">Atención personalizada y confiable</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Mission Section -->
    <section class="bg-blue-700 text-white py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold mb-8 text-center">Nuestra Misión</h2>
        <div class="bg-blue-600 p-8 rounded-lg text-center">
          <p class="text-xl leading-relaxed">
            Brindar soluciones eléctricas de alta calidad, seguras y adaptadas a las necesidades
            actuales, integrando tecnologías limpias y eficientes para contribuir a un futuro más
            sustentable.
          </p>
        </div>
      </div>
    </section>

    <!-- Why Choose Us -->
    <section class="py-16 bg-gray-50">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-blue-700 mb-12 text-center">¿Por Qué Elegirnos?</h2>
        <div class="grid md:grid-cols-2 gap-8">
          <div class="flex gap-4">
            <span class="text-yellow-400 text-3xl font-bold">✓</span>
            <div>
              <h3 class="text-xl font-bold text-blue-700 mb-2">Experiencia Comprobada</h3>
              <p class="text-gray-700">
                Más de 5 años trabajando en proyectos complejos con resultados exitosos
              </p>
            </div>
          </div>
          <div class="flex gap-4">
            <span class="text-yellow-400 text-3xl font-bold">✓</span>
            <div>
              <h3 class="text-xl font-bold text-blue-700 mb-2">Atención Personalizada</h3>
              <p class="text-gray-700">
                Nos adaptamos a cada proyecto y sus necesidades específicas
              </p>
            </div>
          </div>
          <div class="flex gap-4">
            <span class="text-yellow-400 text-3xl font-bold">✓</span>
            <div>
              <h3 class="text-xl font-bold text-blue-700 mb-2">Calidad y Seguridad</h3>
              <p class="text-gray-700">
                Máximos estándares de ejecución y protección en cada instalación
              </p>
            </div>
          </div>
          <div class="flex gap-4">
            <span class="text-yellow-400 text-3xl font-bold">✓</span>
            <div>
              <h3 class="text-xl font-bold text-blue-700 mb-2">Enfoque Sostenible</h3>
              <p class="text-gray-700">
                Soluciones con energías limpias y respetuosas con el ambiente
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
