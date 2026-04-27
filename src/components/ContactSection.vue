<template>
  <section id="kontakt" ref="sectionRef" class="section container">
    <div class="section-heading centered reveal" :class="{ visible }">
      <p class="section-tag">Kontakt</p>
      <h2>Direkter Kontakt</h2>
    </div>

    <div class="contact-list reveal reveal-delay-2" :class="{ visible }">
      <div v-for="contact in contacts" :key="contact.name" class="contact-card">
        <div>
          <span class="contact-label">Name</span>
          <p>{{ contact.name }}</p>
        </div>
        <div>
          <span class="contact-label">Telefon</span>
          <p>{{ contact.phone }}</p>
        </div>
        <div>
          <span class="contact-label">E-Mail</span>
          <p>{{ contact.email }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactSection',
  data() {
    return {
      visible: false,
      observer: null,
      contacts: [
        {
          name: 'Kerem Erguel',
          phone: '+49 123 456789',
          email: 'kerem@example.com',
        },
        {
          name: 'Lena Hoffmann',
          phone: '+49 123 456790',
          email: 'lena@example.com',
        },
        {
          name: 'David Kara',
          phone: '+49 123 456791',
          email: 'david@example.com',
        },
      ],
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

.contact-list {
  display: grid;
  gap: 18px;
}

.contact-card {
  position: relative;
  border-radius: 28px;
  padding: 28px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
  border: 1px solid rgba(108, 181, 128, 0.18);
  background: rgba(255, 255, 255, 0.72);
  box-shadow: 0 18px 60px rgba(65, 106, 72, 0.12);
  backdrop-filter: blur(16px);
}

.contact-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.12), transparent 40%, transparent 60%, rgba(45, 212, 191, 0.08));
  opacity: 0;
  transition: opacity 0.35s ease;
  pointer-events: none;
}

.contact-card:hover::before {
  opacity: 1;
}

.contact-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 70px rgba(65, 106, 72, 0.16);
  border-color: rgba(43, 157, 94, 0.24);
}

.contact-label {
  display: inline-block;
  margin-bottom: 8px;
  color: #2fbd69;
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.12em;
}

.contact-card p {
  margin: 0;
  font-size: 1.08rem;
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

.reveal-delay-2 {
  transition-delay: 0.15s;
}

@media (max-width: 980px) {
  .contact-card {
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

  .contact-card {
    border-radius: 22px;
  }
}
</style>
