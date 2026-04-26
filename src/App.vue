<template>
  <div class="page" :style="pageBackgroundStyle">
    <div class="bg-orb orb-1"></div>
    <div class="bg-orb orb-2"></div>
    <div class="bg-grid"></div>

    <AppHeader />

    <main>
      <PhilosophySection />
      <OffersSection />
      <ProductsSection />
      <BookingSection />
      <ContactSection />
    </main>
  </div>
</template>

<script>
import tennisCourtBackground from './assets/tennis-court-header.jpg'
import AppHeader from './components/AppHeader.vue'
import BookingSection from './components/BookingSection.vue'
import ContactSection from './components/ContactSection.vue'
import OffersSection from './components/OffersSection.vue'
import PhilosophySection from './components/PhilosophySection.vue'
import ProductsSection from './components/ProductsSection.vue'

export default {
  name: 'App',
  components: {
    AppHeader,
    BookingSection,
    ContactSection,
    OffersSection,
    PhilosophySection,
    ProductsSection,
  },
  data() {
    return {
      pageBackgroundStyle: {
        backgroundImage: `url(${tennisCourtBackground})`,
      },
    }
  },
}
</script>

<style scoped>
:global(*) {
  box-sizing: border-box;
}

:global(html) {
  scroll-behavior: smooth;
}

:global(body) {
  margin: 0;
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #081120;
  color: #f8fafc;
}

:global(a) {
  color: inherit;
}

.page {
  position: relative;
  min-height: 100vh;
  overflow: hidden;
  background-position: center;
  background-size: cover;
  background-attachment: fixed;
}

.container {
  width: min(1200px, calc(100% - 48px));
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

.bg-orb {
  position: absolute;
  border-radius: 999px;
  filter: blur(70px);
  opacity: 0.45;
  pointer-events: none;
  animation: floatOrb 13s ease-in-out infinite;
}

.orb-1 {
  width: 320px;
  height: 320px;
  top: 80px;
  left: -80px;
  background: rgba(8, 209, 112, 0.28);
}

.orb-2 {
  width: 360px;
  height: 360px;
  top: 180px;
  right: -90px;
  background: rgba(59, 130, 246, 0.24);
  animation-delay: 2s;
}

.bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.035) 1px, transparent 1px);
  background-size: 34px 34px;
  mask-image: radial-gradient(circle at center, black 36%, transparent 85%);
  pointer-events: none;
}

@keyframes floatOrb {
  0%,
  100% {
    transform: translate3d(0, 0, 0) scale(1);
  }
  50% {
    transform: translate3d(20px, -20px, 0) scale(1.05);
  }
}

@media (max-width: 640px) {
  .container {
    width: min(100% - 28px, 1200px);
  }

  .bg-grid {
    background-size: 24px 24px;
  }
}
</style>
