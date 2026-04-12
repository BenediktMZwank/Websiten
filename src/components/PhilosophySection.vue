<template>
  <section id="philosophie" ref="sectionRef" class="section container">
    <div class="section-heading centered reveal" :class="{ visible }">
      <p class="section-tag">Trainings-Philosophie</p>
      <h2>Fortschritt durch klares, individuelles Coaching</h2>
      <p>
        Gute Entwicklung entsteht nicht zufaellig. Sie entsteht durch Struktur,
        sauberes Feedback und Training, das wirklich zu dir passt.
      </p>
    </div>

    <div class="card-grid">
      <article class="info-card reveal reveal-delay-1" :class="{ visible }">
        <div class="icon-circle">Ziel</div>
        <h3>Individuell</h3>
        <p>
          Jede Einheit wird auf dein Niveau, deine Technik und deine Ziele abgestimmt.
        </p>
      </article>

      <article class="info-card reveal reveal-delay-2" :class="{ visible }">
        <div class="icon-circle">Plan</div>
        <h3>Strukturiert</h3>
        <p>
          Mit klaren Schwerpunkten in Technik, Taktik, Fussarbeit und Spielverstaendnis.
        </p>
      </article>

      <article class="info-card reveal reveal-delay-3" :class="{ visible }">
        <div class="icon-circle">Drive</div>
        <h3>Motivierend</h3>
        <p>
          Anspruchsvoll, positiv und mit sichtbar messbarem Fortschritt im Training.
        </p>
      </article>
    </div>
  </section>
</template>

<script>
export default {
  name: 'PhilosophySection',
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

.section-heading p:last-child,
.info-card p {
  color: rgba(246, 255, 248, 0.92);
  line-height: 1.8;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}

.info-card {
  position: relative;
  padding: 30px;
  border-radius: 28px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
  border: 1px solid rgba(108, 181, 128, 0.18);
  background: rgba(255, 255, 255, 0.7);
  box-shadow: 0 18px 60px rgba(65, 106, 72, 0.12);
  backdrop-filter: blur(16px);
}

.info-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.12), transparent 40%, transparent 60%, rgba(45, 212, 191, 0.08));
  opacity: 0;
  transition: opacity 0.35s ease;
  pointer-events: none;
}

.info-card:hover::before {
  opacity: 1;
}

.info-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 70px rgba(65, 106, 72, 0.16);
  border-color: rgba(43, 157, 94, 0.24);
}

.icon-circle {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  display: grid;
  place-items: center;
  font-size: 0.8rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: #1e5a36;
  background: rgba(121, 231, 148, 0.18);
  margin-bottom: 18px;
}

.info-card h3 {
  margin: 0 0 12px;
  font-size: 1.45rem;
  color: #153824;
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
  .card-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 640px) {
  .container {
    width: min(100% - 28px, 1200px);
  }

  .section {
    padding: 72px 0;
  }

  .info-card {
    border-radius: 22px;
  }
}
</style>
