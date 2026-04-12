<template>
  <section id="probestunde" ref="sectionRef" class="section container">
    <div class="booking-layout">
      <div class="booking-copy reveal reveal-delay-1" :class="{ visible }">
        <p class="section-tag">Probestunde buchen</p>
        <h2>Starte jetzt mit deiner ersten Trainingseinheit</h2>
        <p>
          Trag deine Daten ein und ich melde mich mit einem passenden Termin.
        </p>
      </div>

      <form class="booking-form reveal reveal-delay-2" :class="{ visible }" @submit.prevent="submitForm">
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
            placeholder="Erzaehl kurz von deinem Spielniveau oder deinen Zielen"
          ></textarea>
        </div>

        <button type="submit" class="btn btn-primary full-button magnetic-button">Probestunde anfragen</button>
      </form>
    </div>

    <p v-if="submitted" class="success-message reveal visible">
      Danke! Deine Anfrage wurde erfasst.
    </p>
  </section>
</template>

<script>
export default {
  name: 'BookingSection',
  data() {
    return {
      submitted: false,
      visible: false,
      observer: null,
      form: {
        name: '',
        phone: '',
        email: '',
        message: '',
      },
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

.section-tag {
  display: inline-block;
  margin-bottom: 14px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  font-size: 0.82rem;
  font-weight: 700;
  color: #5eead4;
}

.booking-layout {
  display: grid;
  grid-template-columns: 0.95fr 1.05fr;
  gap: 28px;
  align-items: start;
}

.booking-copy h2 {
  margin: 0;
  font-size: clamp(2rem, 4vw, 3.4rem);
  line-height: 1.05;
  letter-spacing: -0.04em;
}

.booking-copy p {
  color: rgba(226, 232, 240, 0.82);
  line-height: 1.8;
}

.booking-form {
  position: relative;
  padding: 28px;
  border-radius: 28px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.06);
  box-shadow: 0 18px 60px rgba(0, 0, 0, 0.28);
  backdrop-filter: blur(16px);
}

.booking-form::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.12), transparent 40%, transparent 60%, rgba(45, 212, 191, 0.08));
  opacity: 0;
  transition: opacity 0.35s ease;
  pointer-events: none;
}

.booking-form:hover::before {
  opacity: 1;
}

.booking-form:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.34);
  border-color: rgba(94, 234, 212, 0.24);
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

.full-button {
  width: 100%;
}

.success-message {
  margin-top: 18px;
  color: #86efac;
  font-weight: 700;
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

@media (max-width: 980px) {
  .booking-layout,
  .booking-form {
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

  .booking-form {
    border-radius: 22px;
  }
}
</style>
