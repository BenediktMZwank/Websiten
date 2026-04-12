<template>
  <div class="page">
    <div class="bg-orb orb-1"></div>
    <div class="bg-orb orb-2"></div>
    <div class="bg-grid"></div>

    <header class="hero">
      <nav class="nav container reveal reveal-delay-1" :class="{ visible: visibleSections.nav }">
        <div class="logo">Trainer H</div>
        <div class="nav-links">
          <a href="#philosophie">Philosophie</a>
          <a href="#angebote">Angebote</a>
          <a href="#kontakt">Kontakt</a>
          <a href="#probestunde" class="btn btn-small btn-primary magnetic-button">Probestunde</a>
        </div>
      </nav>

      <section class="hero-content container">
        <div class="hero-text reveal reveal-delay-1" :class="{ visible: visibleSections.hero }">
          <p class="eyebrow">Personal Tennis Training</p>
          <h1>Modernes Tennistraining für Technik, Matchstärke und Selbstvertrauen</h1>
          <p class="subtitle">
            Individuelles Coaching für Anfänger, Fortgeschrittene und ambitionierte
            Spieler – mit klarer Struktur, spürbarem Fortschritt und einem modernen Trainingserlebnis.
          </p>

          <div class="hero-actions reveal reveal-delay-2" :class="{ visible: visibleSections.hero }">
            <a href="#probestunde" class="btn btn-primary magnetic-button">Jetzt Probestunde buchen</a>
            <a href="#angebote" class="btn btn-ghost">Preise ansehen</a>
          </div>

          <div class="hero-stats reveal reveal-delay-3" :class="{ visible: visibleSections.hero }">
            <div class="stat-card glass-card floating-card">
              <span class="stat-number">1:1</span>
              <span class="stat-label">Individuelles Coaching</span>
            </div>
            <div class="stat-card glass-card floating-card float-delay-2">
              <span class="stat-number">100%</span>
              <span class="stat-label">Auf dein Niveau angepasst</span>
            </div>
            <div class="stat-card glass-card floating-card float-delay-3">
              <span class="stat-number">🎾</span>
              <span class="stat-label">Technik, Taktik, Athletik</span>
            </div>
          </div>
        </div>

        <div class="hero-panel glass-card reveal reveal-delay-2 floating-card" :class="{ visible: visibleSections.hero }">
          <div class="panel-badge">Dein Fokus</div>
          <h3>Gezielt trainieren statt nur Bälle schlagen</h3>
          <ul>
            <li><span>🎾</span> Einzeltraining mit persönlichem Fokus</li>
            <li><span>⚡</span> Matchvorbereitung und Spielsituationen</li>
            <li><span>💪</span> Beweglichkeit, Fußarbeit und Athletik</li>
            <li><span>🧠</span> Mentale Stärke und Konstanz im Spiel</li>
          </ul>
        </div>
      </section>
    </header>

    <main>
      <section id="philosophie" class="section container" ref="philosophieSection">
        <div class="section-heading centered reveal" :class="{ visible: visibleSections.philosophie }">
          <p class="section-tag">Trainings-Philosophie</p>
          <h2>Fortschritt durch klares, individuelles Coaching</h2>
          <p>
            Gute Entwicklung entsteht nicht zufällig. Sie entsteht durch Struktur,
            sauberes Feedback und Training, das wirklich zu dir passt.
          </p>
        </div>

        <div class="card-grid">
          <article class="info-card reveal reveal-delay-1" :class="{ visible: visibleSections.philosophie }">
            <div class="icon-circle">🎯</div>
            <h3>Individuell</h3>
            <p>
              Jede Einheit wird auf dein Niveau, deine Technik und deine Ziele abgestimmt.
            </p>
          </article>

          <article class="info-card reveal reveal-delay-2" :class="{ visible: visibleSections.philosophie }">
            <div class="icon-circle">📈</div>
            <h3>Strukturiert</h3>
            <p>
              Mit klaren Schwerpunkten in Technik, Taktik, Fußarbeit und Spielverständnis.
            </p>
          </article>

          <article class="info-card reveal reveal-delay-3" :class="{ visible: visibleSections.philosophie }">
            <div class="icon-circle">🔥</div>
            <h3>Motivierend</h3>
            <p>
              Anspruchsvoll, positiv und mit sichtbar messbarem Fortschritt im Training.
            </p>
          </article>
        </div>
      </section>

      <section id="angebote" class="section section-soft" ref="angeboteSection">
        <div class="container">
          <div class="section-heading centered reveal" :class="{ visible: visibleSections.angebote }">
            <p class="section-tag">Angebote & Preise</p>
            <h2>Das passende Training für dein Ziel</h2>
          </div>

          <div class="pricing-grid">
            <article class="price-card reveal reveal-delay-1" :class="{ visible: visibleSections.angebote }">
              <p class="plan-name">Einzelstunde</p>
              <h3>Perfekt zum Einstieg</h3>
              <p class="price">49 €</p>
              <p class="price-text">60 Minuten persönliches 1:1 Training</p>
            </article>

            <article class="price-card featured reveal reveal-delay-2" :class="{ visible: visibleSections.angebote }">
              <span class="badge">Am beliebtesten</span>
              <p class="plan-name">5er Paket</p>
              <h3>Konstant besser werden</h3>
              <p class="price">225 €</p>
              <p class="price-text">Mehr Kontinuität, mehr Entwicklung, besserer Preis</p>
            </article>

            <article class="price-card reveal reveal-delay-3" :class="{ visible: visibleSections.angebote }">
              <p class="plan-name">10er Paket</p>
              <h3>Für nachhaltigen Fortschritt</h3>
              <p class="price">430 €</p>
              <p class="price-text">Langfristiger Trainingsplan mit persönlichem Fokus</p>
            </article>
          </div>
        </div>
      </section>

      <section id="probestunde" class="section container" ref="bookingSection">
        <div class="booking-layout">
          <div class="booking-copy reveal reveal-delay-1" :class="{ visible: visibleSections.booking }">
            <p class="section-tag">Probestunde buchen</p>
            <h2>Starte jetzt mit deiner ersten Trainingseinheit</h2>
            <p>
              Trag deine Daten ein und ich melde mich mit einem passenden Termin.
            </p>
          </div>

          <form class="booking-form reveal reveal-delay-2" :class="{ visible: visibleSections.booking }" @submit.prevent="submitForm">
            <div class="form-group">
              <label for="name">Name</label>
              <input id="name" v-model="form.name" type="text" placeholder="Dein Name" required />
            </div>

            <div class="form-group">
              <label for="phone">Telefonnummer</label>
              <input id="phone" v-model="form.phone" type="tel" placeholder="0123 456789" required />
            </div>

            <div class="form-group full-width">
              <label for="email">E-Mail</label>
              <input id="email" v-model="form.email" type="email" placeholder="deinname@mail.de" required />
            </div>

            <div class="form-group full-width">
              <label for="message">Nachricht</label>
              <textarea
                id="message"
                v-model="form.message"
                rows="5"
                placeholder="Erzähl kurz von deinem Spielniveau oder deinen Zielen"
              ></textarea>
            </div>

            <button type="submit" class="btn btn-primary full-button magnetic-button">Probestunde anfragen</button>
          </form>
        </div>

        <p v-if="submitted" class="success-message reveal visible">
          Danke! Deine Anfrage wurde erfasst. 🎉
        </p>
      </section>

      <section id="kontakt" class="section container" ref="kontaktSection">
        <div class="section-heading centered reveal" :class="{ visible: visibleSections.kontakt }">
          <p class="section-tag">Kontakt</p>
          <h2>Direkter Kontakt</h2>
        </div>

        <div class="contact-card reveal reveal-delay-2" :class="{ visible: visibleSections.kontakt }">
          <div>
            <span class="contact-label">Name</span>
            <p>Trainer H</p>
          </div>
          <div>
            <span class="contact-label">Telefon</span>
            <p>+49 123 456789</p>
          </div>
          <div>
            <span class="contact-label">E-Mail</span>
            <p>trainerh@example.com</p>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      submitted: false,
      form: {
        name: '',
        phone: '',
        email: '',
        message: '',
      },
      visibleSections: {
        nav: false,
        hero: false,
        philosophie: false,
        angebote: false,
        booking: false,
        kontakt: false,
      },
      observer: null,
    }
  },
  mounted() {
    requestAnimationFrame(() => {
      this.visibleSections.nav = true
      this.visibleSections.hero = true
    })

    const options = {
      threshold: 0.18,
      rootMargin: '0px 0px -80px 0px',
    }

    this.observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) return

        if (entry.target === this.$refs.philosophieSection) {
          this.visibleSections.philosophie = true
        }
        if (entry.target === this.$refs.angeboteSection) {
          this.visibleSections.angebote = true
        }
        if (entry.target === this.$refs.bookingSection) {
          this.visibleSections.booking = true
        }
        if (entry.target === this.$refs.kontaktSection) {
          this.visibleSections.kontakt = true
        }
      })
    }, options)

    const sections = [
      this.$refs.philosophieSection,
      this.$refs.angeboteSection,
      this.$refs.bookingSection,
      this.$refs.kontaktSection,
    ]

    sections.forEach((section) => {
      if (section) this.observer.observe(section)
    })
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect()
    }
  },
  methods: {
    submitForm() {
      console.log('Formulardaten:', this.form)
      this.submitted = true
      this.form = {
        name: '',
        phone: '',
        email: '',
        message: '',
      }
    },
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
  background:
    radial-gradient(circle at top left, rgba(45, 212, 191, 0.16), transparent 32%),
    radial-gradient(circle at top right, rgba(59, 130, 246, 0.18), transparent 26%),
    linear-gradient(180deg, #081120 0%, #0b1427 36%, #0d172a 100%);
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
  background: rgba(45, 212, 191, 0.28);
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

.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 28px 0 56px;
}

.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  margin-bottom: 64px;
}

.logo {
  font-size: 1.7rem;
  font-weight: 800;
  letter-spacing: -0.03em;
}

.nav-links {
  display: flex;
  gap: 28px;
  align-items: center;
  flex-wrap: wrap;
}

.nav-links a {
  text-decoration: none;
  color: rgba(248, 250, 252, 0.9);
  font-weight: 500;
  transition: color 0.25s ease, transform 0.25s ease;
}

.nav-links a:hover {
  color: #5eead4;
  transform: translateY(-1px);
}

.hero-content {
  flex: 1;
  display: grid;
  grid-template-columns: 1.25fr 0.85fr;
  gap: 40px;
  align-items: center;
  position: relative;
  z-index: 2;
}

.eyebrow,
.section-tag {
  display: inline-block;
  margin-bottom: 14px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  font-size: 0.82rem;
  font-weight: 700;
  color: #5eead4;
}

.hero-text h1 {
  margin: 0;
  font-size: clamp(3rem, 7vw, 5.4rem);
  line-height: 0.96;
  letter-spacing: -0.05em;
  max-width: 860px;
}

.subtitle {
  margin-top: 24px;
  max-width: 720px;
  font-size: 1.14rem;
  line-height: 1.8;
  color: rgba(226, 232, 240, 0.88);
}

.hero-actions {
  margin-top: 32px;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.hero-stats {
  margin-top: 28px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 14px;
  max-width: 760px;
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 14px 22px;
  border-radius: 999px;
  text-decoration: none;
  font-weight: 700;
  border: 1px solid transparent;
  cursor: pointer;
  transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease, background 0.25s ease;
}

.btn-primary {
  background: linear-gradient(135deg, #2dd4bf, #22c55e);
  color: #04111d;
  box-shadow: 0 12px 30px rgba(34, 197, 94, 0.22);
}

.btn-primary:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 18px 36px rgba(34, 197, 94, 0.32);
}

.btn-ghost {
  background: rgba(255, 255, 255, 0.06);
  color: #f8fafc;
  border-color: rgba(255, 255, 255, 0.14);
  backdrop-filter: blur(10px);
}

.btn-ghost:hover {
  transform: translateY(-2px);
  border-color: rgba(94, 234, 212, 0.34);
}

.btn-small {
  padding: 11px 18px;
}

.glass-card,
.info-card,
.price-card,
.booking-form,
.contact-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.06);
  box-shadow: 0 18px 60px rgba(0, 0, 0, 0.28);
  backdrop-filter: blur(16px);
}

.hero-panel {
  padding: 32px;
  border-radius: 28px;
  position: relative;
  overflow: hidden;
}

.hero-panel::before,
.info-card::before,
.price-card::before,
.booking-form::before,
.contact-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.12), transparent 40%, transparent 60%, rgba(45, 212, 191, 0.08));
  opacity: 0;
  transition: opacity 0.35s ease;
  pointer-events: none;
}

.hero-panel:hover::before,
.info-card:hover::before,
.price-card:hover::before,
.booking-form:hover::before,
.contact-card:hover::before {
  opacity: 1;
}

.panel-badge {
  display: inline-flex;
  padding: 8px 14px;
  border-radius: 999px;
  background: rgba(45, 212, 191, 0.14);
  color: #99f6e4;
  font-size: 0.82rem;
  font-weight: 700;
  margin-bottom: 18px;
}

.hero-panel h3 {
  margin: 0 0 18px;
  font-size: 1.7rem;
  line-height: 1.2;
}

.hero-panel ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 16px;
}

.hero-panel li {
  display: flex;
  align-items: center;
  gap: 12px;
  color: rgba(248, 250, 252, 0.92);
}

.stat-card {
  padding: 18px;
  border-radius: 22px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.stat-number {
  font-size: 1.5rem;
  font-weight: 800;
}

.stat-label {
  font-size: 0.92rem;
  color: rgba(226, 232, 240, 0.82);
}

.section {
  padding: 96px 0;
  position: relative;
  z-index: 2;
}

.section-soft {
  background: linear-gradient(180deg, rgba(15, 23, 42, 0.42), rgba(8, 17, 32, 0.14));
  border-top: 1px solid rgba(255, 255, 255, 0.06);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
}

.centered {
  text-align: center;
}

.section-heading {
  max-width: 760px;
  margin: 0 auto 42px;
}

.section-heading h2,
.booking-copy h2 {
  margin: 0;
  font-size: clamp(2rem, 4vw, 3.4rem);
  line-height: 1.05;
  letter-spacing: -0.04em;
}

.section-heading p:last-child,
.booking-copy p,
.info-card p,
.price-text,
.plan-name {
  color: rgba(226, 232, 240, 0.82);
  line-height: 1.8;
}

.card-grid,
.pricing-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}

.info-card,
.price-card {
  position: relative;
  padding: 30px;
  border-radius: 28px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.info-card:hover,
.price-card:hover,
.hero-panel:hover,
.contact-card:hover,
.booking-form:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.34);
  border-color: rgba(94, 234, 212, 0.24);
}

.icon-circle {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  display: grid;
  place-items: center;
  font-size: 1.4rem;
  background: rgba(45, 212, 191, 0.12);
  margin-bottom: 18px;
}

.info-card h3,
.price-card h3 {
  margin: 0 0 12px;
  font-size: 1.45rem;
}

.price {
  margin: 10px 0 6px;
  font-size: 3rem;
  font-weight: 800;
  letter-spacing: -0.04em;
}

.featured {
  position: relative;
  transform: translateY(-8px);
  border-color: rgba(45, 212, 191, 0.42);
  background: linear-gradient(180deg, rgba(45, 212, 191, 0.12), rgba(255, 255, 255, 0.07));
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
  background: #2dd4bf;
  color: #06202b;
  font-size: 0.78rem;
  font-weight: 800;
}

.booking-layout {
  display: grid;
  grid-template-columns: 0.95fr 1.05fr;
  gap: 28px;
  align-items: start;
}

.booking-form {
  position: relative;
  padding: 28px;
  border-radius: 28px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  margin-bottom: 8px;
  font-weight: 600;
  color: rgba(248, 250, 252, 0.94);
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 14px 16px;
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(6, 12, 24, 0.65);
  color: #f8fafc;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.25s ease, box-shadow 0.25s ease, transform 0.25s ease;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(148, 163, 184, 0.8);
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: rgba(45, 212, 191, 0.7);
  box-shadow: 0 0 0 4px rgba(45, 212, 191, 0.12);
  transform: translateY(-1px);
}

.full-width {
  grid-column: 1 / -1;
}

.full-button {
  width: 100%;
}

.success-message {
  margin-top: 18px;
  color: #86efac;
  font-weight: 700;
}

.contact-card {
  position: relative;
  border-radius: 28px;
  padding: 28px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.contact-label {
  display: inline-block;
  margin-bottom: 8px;
  color: #5eead4;
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.12em;
}

.contact-card p {
  margin: 0;
  font-size: 1.08rem;
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

.floating-card {
  animation: floatCard 6.8s ease-in-out infinite;
}

.float-delay-2 {
  animation-delay: 1.1s;
}

.float-delay-3 {
  animation-delay: 2.2s;
}

.magnetic-button {
  position: relative;
  overflow: hidden;
}

.magnetic-button::after {
  content: '';
  position: absolute;
  inset: -120% auto auto -20%;
  width: 60%;
  height: 300%;
  transform: rotate(20deg);
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.22), transparent);
  transition: transform 0.7s ease;
}

.magnetic-button:hover::after {
  transform: translateX(260%) rotate(20deg);
}

@keyframes floatCard {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
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

@media (max-width: 980px) {
  .hero-content,
  .booking-layout,
  .card-grid,
  .pricing-grid,
  .contact-card,
  .hero-stats,
  .booking-form {
    grid-template-columns: 1fr;
  }

  .hero {
    min-height: auto;
    padding-bottom: 28px;
  }

  .nav {
    margin-bottom: 36px;
    align-items: flex-start;
    flex-direction: column;
  }

  .nav-links {
    gap: 16px;
  }

  .hero-text h1 {
    font-size: clamp(2.5rem, 11vw, 4rem);
  }

  .featured,
  .featured:hover {
    transform: none;
  }

  .floating-card {
    animation-duration: 7.4s;
  }
}

@media (max-width: 640px) {
  .container {
    width: min(100% - 28px, 1200px);
  }

  .section {
    padding: 72px 0;
  }

  .hero-panel,
  .info-card,
  .price-card,
  .booking-form,
  .contact-card {
    border-radius: 22px;
  }

  .bg-grid {
    background-size: 24px 24px;
  }
}
</style>

