<template>
  <section id="angebote" ref="sectionRef" class="section section-soft">
    <div class="container">
      <div class="section-heading centered reveal" :class="{ visible }">
        <p class="section-tag">Angebote & Preise</p>
        <h2>Das passende Training fuer dein Ziel</h2>
      </div>

      <div class="pricing-grid">
        <article class="price-card reveal reveal-delay-1" :class="{ visible }">
          <p class="plan-name">Einzelstunde</p>
          <h3>Perfekt zum Einstieg</h3>
          <p class="price">49 EUR</p>
          <p class="price-text">60 Minuten persoenliches 1:1 Training</p>
        </article>

        <article class="price-card featured reveal reveal-delay-2" :class="{ visible }">
          <span class="badge">Am beliebtesten</span>
          <p class="plan-name">5er Paket</p>
          <h3>Konstant besser werden</h3>
          <p class="price">225 EUR</p>
          <p class="price-text">Mehr Kontinuitaet, mehr Entwicklung, besserer Preis</p>
        </article>

        <article class="price-card reveal reveal-delay-3" :class="{ visible }">
          <p class="plan-name">10er Paket</p>
          <h3>Fuer nachhaltigen Fortschritt</h3>
          <p class="price">430 EUR</p>
          <p class="price-text">Langfristiger Trainingsplan mit persoenlichem Fokus</p>
        </article>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'OffersSection',
  data() {
    return {
      visible: false,
      observer: null,
    }
  },
  mounted() {
    this.observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (!entry.isIntersecting) return
          this.visible = true
          this.observer?.disconnect()
        })
      },
      {
        threshold: 0.18,
        rootMargin: '0px 0px -80px 0px',
      },
    )

    if (this.$refs.sectionRef) {
      this.observer.observe(this.$refs.sectionRef)
    }
  },
  beforeUnmount() {
    this.observer?.disconnect()
  },
}
</script>

<style scoped>
.container {
  width: min(1200px, calc(100% - 48px));
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

.section {
  padding: 96px 0;
  position: relative;
  z-index: 2;
}

.section-soft {
  background: linear-gradient(180deg, rgba(233, 255, 237, 0.9), rgba(222, 248, 227, 0.5));
  border-top: 1px solid rgba(86, 164, 108, 0.1);
  border-bottom: 1px solid rgba(86, 164, 108, 0.1);
}

.centered {
  text-align: center;
}

.section-heading {
  max-width: 760px;
  margin: 0 auto 42px;
}

.section-tag {
  display: inline-block;
  margin-bottom: 14px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  font-size: 0.82rem;
  font-weight: 700;
  color: #2b9d5e;
}

.section-heading h2 {
  margin: 0;
  font-size: clamp(2rem, 4vw, 3.4rem);
  line-height: 1.05;
  letter-spacing: -0.04em;
  color: #f7fff8;
  text-shadow: 0 8px 24px rgba(12, 34, 21, 0.32);
}

.pricing-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}

.price-card {
  position: relative;
  padding: 30px;
  border-radius: 28px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
  border: 1px solid rgba(108, 181, 128, 0.18);
  background: rgba(255, 255, 255, 0.72);
  box-shadow: 0 18px 60px rgba(65, 106, 72, 0.12);
  backdrop-filter: blur(16px);
}

.price-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.12), transparent 40%, transparent 60%, rgba(45, 212, 191, 0.08));
  opacity: 0;
  transition: opacity 0.35s ease;
  pointer-events: none;
}

.price-card:hover::before {
  opacity: 1;
}

.price-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 70px rgba(65, 106, 72, 0.16);
  border-color: rgba(43, 157, 94, 0.24);
}

.price-card h3 {
  margin: 0 0 12px;
  font-size: 1.45rem;
  color: #153824;
}

.price {
  margin: 10px 0 6px;
  font-size: 3rem;
  font-weight: 800;
  letter-spacing: -0.04em;
  color: #133321;
}

.price-text,
.plan-name {
  color: rgba(246, 255, 248, 0.92);
  line-height: 1.8;
}

.featured {
  position: relative;
  transform: translateY(-8px);
  border-color: rgba(76, 196, 110, 0.35);
  background: linear-gradient(180deg, rgba(151, 255, 175, 0.3), rgba(255, 255, 255, 0.76));
}

.featured:hover {
  transform: translateY(-14px) scale(1.01);
}

.badge {
  position: absolute;
  top: 18px;
  right: 18px;
  padding: 8px 12px;
  border-radius: 999px;
  background: #8cff9b;
  color: #0b2b17;
  font-size: 0.78rem;
  font-weight: 800;
}

.reveal {
  opacity: 0;
  transform: translateY(42px) scale(0.985);
  transition: opacity 0.9s cubic-bezier(0.22, 1, 0.36, 1), transform 0.9s cubic-bezier(0.22, 1, 0.36, 1);
  will-change: transform, opacity;
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.reveal-delay-1 {
  transition-delay: 0.05s;
}

.reveal-delay-2 {
  transition-delay: 0.15s;
}

.reveal-delay-3 {
  transition-delay: 0.26s;
}

@media (max-width: 980px) {
  .pricing-grid {
    grid-template-columns: 1fr;
  }

  .featured,
  .featured:hover {
    transform: none;
  }
}

@media (max-width: 640px) {
  .container {
    width: min(100% - 28px, 1200px);
  }

  .section {
    padding: 72px 0;
  }

  .price-card {
    border-radius: 22px;
  }
}
</style>
