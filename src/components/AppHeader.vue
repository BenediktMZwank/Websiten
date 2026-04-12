<template>
  <header class="hero">
    <nav class="nav container reveal reveal-delay-1" :class="{ visible: visibleNav }">
      <div class="logo">Trainer H</div>
      <div class="nav-links">
        <a href="#philosophie">Philosophie</a>
        <a href="#angebote">Angebote</a>
        <a href="#kontakt">Kontakt</a>
        <a href="#probestunde" class="btn btn-small btn-primary magnetic-button">Probestunde</a>
      </div>
    </nav>

    <section class="hero-content container">
      <div class="hero-text reveal reveal-delay-1" :class="{ visible: visibleHero }">
        <p class="eyebrow">Personal Tennis Training</p>
        <h1>Modernes Tennistraining fÃ¼r Technik, MatchstÃ¤rke und Selbstvertrauen</h1>
        <p class="subtitle">
          Individuelles Coaching fÃ¼r AnfÃ¤nger, Fortgeschrittene und ambitionierte
          Spieler â€“ mit klarer Struktur, spÃ¼rbarem Fortschritt und einem modernen Trainingserlebnis.
        </p>

        <div class="hero-actions reveal reveal-delay-2" :class="{ visible: visibleHero }">
          <a href="#probestunde" class="btn btn-primary magnetic-button">Jetzt Probestunde buchen</a>
          <a href="#angebote" class="btn btn-ghost">Preise ansehen</a>
        </div>

        <div class="hero-stats reveal reveal-delay-3" :class="{ visible: visibleHero }">
          <div class="stat-card glass-card floating-card">
            <span class="stat-number">1:1</span>
            <span class="stat-label">Individuelles Coaching</span>
          </div>
          <div class="stat-card glass-card floating-card float-delay-2">
            <span class="stat-number">100%</span>
            <span class="stat-label">Auf dein Niveau angepasst</span>
          </div>
          <div class="stat-card glass-card floating-card float-delay-3">
            <span class="stat-number">ðŸŽ¾</span>
            <span class="stat-label">Technik, Taktik, Athletik</span>
          </div>
        </div>
      </div>

      <div class="hero-panel glass-card reveal reveal-delay-2 floating-card" :class="{ visible: visibleHero }">
        <div class="panel-badge">Dein Fokus</div>
        <h3>Gezielt trainieren statt nur BÃ¤lle schlagen</h3>
        <ul>
          <li><span>ðŸŽ¾</span> Einzeltraining mit persÃ¶nlichem Fokus</li>
          <li><span>âš¡</span> Matchvorbereitung und Spielsituationen</li>
          <li><span>ðŸ’ª</span> Beweglichkeit, FuÃŸarbeit und Athletik</li>
          <li><span>ðŸ§ </span> Mentale StÃ¤rke und Konstanz im Spiel</li>
        </ul>
      </div>
    </section>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      visibleNav: false,
      visibleHero: false,
    }
  },
  mounted() {
    requestAnimationFrame(() => {
      this.visibleNav = true
      this.visibleHero = true
    })
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

.eyebrow {
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

.glass-card {
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
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.hero-panel::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.12), transparent 40%, transparent 60%, rgba(45, 212, 191, 0.08));
  opacity: 0;
  transition: opacity 0.35s ease;
  pointer-events: none;
}

.hero-panel:hover::before {
  opacity: 1;
}

.hero-panel:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.34);
  border-color: rgba(94, 234, 212, 0.24);
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

@media (max-width: 980px) {
  .hero-content,
  .hero-stats {
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

  .floating-card {
    animation-duration: 7.4s;
  }
}

@media (max-width: 640px) {
  .container {
    width: min(100% - 28px, 1200px);
  }

  .hero-panel {
    border-radius: 22px;
  }
}
</style>
