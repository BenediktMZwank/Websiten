<template>
  <section id="probestunde" ref="sectionRef" class="section container">
    <div class="booking-shell reveal reveal-delay-1" :class="{ visible }">
      <div class="court-overlay"></div>

      <div class="booking-copy">
        <p class="section-tag">Unser Trainerteam</p>
        <h2>Drei Trainer, drei Perspektiven, ein gemeinsames Ziel</h2>
        <p>
          Lerne unser Team kennen und waehle fuer deine Trainingseinheit den Trainer,
          der am besten zu deinem Stil und deinem Ziel passt.
        </p>
      </div>

      <div class="trainer-grid">
        <article v-for="trainer in trainers" :key="trainer.name" class="trainer-card reveal" :class="{ visible }">
          <div class="trainer-image">
            <span>Bild Platzhalter</span>
          </div>
          <div class="trainer-meta">
            <h3>{{ trainer.name }}</h3>
            <p class="trainer-age">{{ trainer.age }} Jahre</p>
            <p class="trainer-focus">{{ trainer.focus }}</p>
          </div>
        </article>
      </div>

      <div class="booking-panel reveal reveal-delay-2" :class="{ visible }">
        <div class="panel-copy">
          <p class="section-tag small">Training buchen</p>
          <h3>Wunschtrainer auswaehlen</h3>
          <p>
            Waehl deinen Trainer im Dropdown und schick uns direkt deine Anfrage.
          </p>
        </div>

        <form ref="bookingForm" class="booking-form" @submit.prevent="submitForm">
          <div class="form-group">
            <label for="trainer">Trainer</label>
            <select id="trainer" v-model="form.trainer" name="trainer" required>
              <option disabled value="">Bitte Trainer auswaehlen</option>
              <option v-for="trainer in trainers" :key="trainer.name" :value="trainer.name">
                {{ trainer.name }}
              </option>
            </select>
          </div>

          <div class="form-group">
            <label for="name">Name</label>
            <input id="name" v-model="form.name" name="name" type="text" placeholder="Dein Name" required />
          </div>

          <div class="form-group">
            <label for="phone">Telefonnummer</label>
            <input id="phone" v-model="form.phone" name="phone" type="tel" placeholder="0123 456789" required />
          </div>

          <div class="form-group">
            <label for="email">E-Mail</label>
            <input id="email" v-model="form.email" name="email" type="email" placeholder="deinname@mail.de" required />
          </div>

          <div class="form-group full-width">
            <label for="message">Nachricht</label>
            <textarea
              id="message"
              v-model="form.message"
              name="message"
              rows="4"
              placeholder="Erzaehl kurz, was du trainieren moechtest"
            ></textarea>
          </div>

          <input type="hidden" name="site_name" value="MegoPlayTennis" />

          <button type="submit" class="btn btn-primary full-button magnetic-button" :disabled="isSubmitting">
            {{ isSubmitting ? 'Anfrage wird gesendet...' : 'Training buchen' }}
          </button>
        </form>
      </div>
    </div>

    <p v-if="submitted" class="success-message reveal visible">
      Danke! Deine Anfrage wurde erfasst.
    </p>

    <p v-if="errorMessage" class="error-message reveal visible">
      {{ errorMessage }}
    </p>
  </section>
</template>

<script>
import emailjs from '@emailjs/browser'

export default {
  name: 'BookingSection',
  data() {
    return {
      submitted: false,
      isSubmitting: false,
      visible: false,
      errorMessage: '',
      observer: null,
      trainers: [
        {
          name: 'Kerem Ergül',
          age: 26,
          focus: 'Techniktraining, Matchpraxis und individuelles Feedback.',
        },
        {
          name: 'Lena Hoffmann',
          age: 29,
          focus: 'Konstanz, Beinarbeit und ruhige Aufbauarbeit fuer jedes Niveau.',
        },
        {
          name: 'David Kara',
          age: 31,
          focus: 'Athletik, Spielintelligenz und mutiges Offensivspiel.',
        },
      ],
      form: {
        trainer: '',
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
    resetForm() {
      this.form = {
        trainer: '',
        name: '',
        phone: '',
        email: '',
        message: '',
      }
    },
    async submitForm() {
      this.errorMessage = ''
      this.submitted = false

      const serviceId = import.meta.env.VITE_EMAILJS_SERVICE_ID
      const templateId = import.meta.env.VITE_EMAILJS_TEMPLATE_ID
      const publicKey = import.meta.env.VITE_EMAILJS_PUBLIC_KEY

      if (!serviceId || !templateId || !publicKey) {
        this.errorMessage = 'EmailJS ist noch nicht fertig konfiguriert. Bitte trage die Env-Werte ein.'
        return
      }

      if (!this.$refs.bookingForm) {
        this.errorMessage = 'Das Buchungsformular konnte nicht gefunden werden.'
        return
      }

      try {
        this.isSubmitting = true

        await emailjs.sendForm(serviceId, templateId, this.$refs.bookingForm, {
          publicKey,
        })

        this.submitted = true
        this.resetForm()
      } catch (error) {
        console.error('EmailJS Versand fehlgeschlagen:', error)
        this.errorMessage = 'Deine Anfrage konnte gerade nicht gesendet werden. Bitte versuche es erneut.'
      } finally {
        this.isSubmitting = false
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

.booking-shell {
  position: relative;
  overflow: hidden;
  padding: 42px;
  border-radius: 36px;
  border: 1px solid rgba(157, 255, 187, 0.16);
  background:
    linear-gradient(180deg, rgba(24, 107, 63, 0.96), rgba(13, 67, 40, 0.98)),
    radial-gradient(circle at top right, rgba(181, 255, 186, 0.16), transparent 28%),
    radial-gradient(circle at bottom left, rgba(116, 255, 161, 0.14), transparent 30%);
  box-shadow: 0 30px 90px rgba(0, 0, 0, 0.28);
}

.court-overlay {
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0.58;
  background:
    linear-gradient(rgba(247, 255, 245, 0.3) 0 0) center 50% / 78% 2px no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.34) 0 0) 50% 50% / 2px 70% no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.3) 0 0) 50% 29% / 46% 2px no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.3) 0 0) 50% 71% / 46% 2px no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.34) 0 0) 16% 50% / 2px 70% no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.34) 0 0) 84% 50% / 2px 70% no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.28) 0 0) 50% 14% / 78% 2px no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.28) 0 0) 50% 86% / 78% 2px no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.24) 0 0) 11% 50% / 2px 78% no-repeat,
    linear-gradient(rgba(247, 255, 245, 0.24) 0 0) 89% 50% / 2px 78% no-repeat,
    linear-gradient(90deg, rgba(255, 255, 255, 0.05) 0, rgba(255, 255, 255, 0) 45%, rgba(255, 255, 255, 0.05) 100%),
    radial-gradient(circle at top left, rgba(158, 255, 170, 0.14), transparent 26%);
}

.court-overlay::before,
.court-overlay::after {
  content: '';
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 84%;
  border-radius: 999px;
  border: 2px solid rgba(247, 255, 245, 0.22);
}

.court-overlay::before {
  top: -34%;
  height: 52%;
}

.court-overlay::after {
  bottom: -34%;
  height: 52%;
}

.booking-copy,
.trainer-grid,
.booking-panel {
  position: relative;
  z-index: 1;
}

.section-tag {
  display: inline-block;
  margin-bottom: 14px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  font-size: 0.82rem;
  font-weight: 700;
  color: #dcffe5;
}

.section-tag.small {
  margin-bottom: 10px;
  font-size: 0.72rem;
}

.booking-copy {
  max-width: 760px;
  margin-bottom: 34px;
}

.booking-copy h2 {
  margin: 0;
  font-size: clamp(2rem, 4vw, 3.3rem);
  line-height: 1.05;
  letter-spacing: -0.04em;
}

.booking-copy p:last-child,
.panel-copy p,
.trainer-focus {
  color: rgba(244, 255, 247, 0.9);
  line-height: 1.8;
}

.trainer-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-bottom: 28px;
}

.trainer-card,
.booking-panel {
  position: relative;
  border: 1px solid rgba(210, 255, 225, 0.14);
  background: rgba(255, 255, 255, 0.06);
  box-shadow: 0 18px 60px rgba(0, 0, 0, 0.24);
  backdrop-filter: blur(14px);
}

.trainer-card {
  border-radius: 28px;
  overflow: hidden;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.trainer-card:hover,
.booking-panel:hover {
  transform: translateY(-6px);
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.28);
  border-color: rgba(185, 255, 203, 0.3);
}

.trainer-image {
  min-height: 240px;
  display: grid;
  place-items: center;
  color: rgba(234, 255, 238, 0.88);
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  background:
    radial-gradient(circle at 50% 20%, rgba(255, 255, 255, 0.18), transparent 24%),
    linear-gradient(180deg, rgba(154, 255, 182, 0.18), rgba(16, 55, 34, 0.24)),
    linear-gradient(135deg, rgba(9, 32, 22, 0.4), rgba(38, 110, 62, 0.36));
}

.trainer-meta {
  padding: 22px;
}

.trainer-meta h3 {
  margin: 0 0 8px;
  font-size: 1.45rem;
}

.trainer-age {
  margin: 0 0 10px;
  color: #d9ffe3;
  font-weight: 700;
}

.trainer-focus {
  margin: 0;
}

.booking-panel {
  border-radius: 30px;
  padding: 28px;
  display: grid;
  grid-template-columns: 0.8fr 1.2fr;
  gap: 24px;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.panel-copy h3 {
  margin: 0 0 10px;
  font-size: 1.8rem;
}

.booking-form {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  margin-bottom: 8px;
  font-weight: 600;
  color: rgba(248, 255, 250, 0.98);
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  padding: 14px 16px;
  border-radius: 16px;
  border: 1px solid rgba(210, 255, 225, 0.14);
  background: rgba(5, 24, 16, 0.62);
  color: #f8fafc;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.25s ease, box-shadow 0.25s ease, transform 0.25s ease;
}

.booking-copy h2,
.panel-copy h3,
.trainer-meta h3,
.success-message {
  color: #f8fff9;
}

.form-group select {
  appearance: none;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(196, 226, 201, 0.7);
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  border-color: rgba(132, 255, 164, 0.7);
  box-shadow: 0 0 0 4px rgba(115, 255, 155, 0.12);
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
  background: linear-gradient(135deg, #8cff9b, #4ed07f);
  color: #082013;
  box-shadow: 0 12px 30px rgba(78, 208, 127, 0.24);
}

.btn-primary:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 18px 36px rgba(78, 208, 127, 0.34);
}

.full-button {
  width: 100%;
}

.full-button:disabled {
  cursor: wait;
  opacity: 0.72;
}

.success-message {
  margin-top: 18px;
  color: #b9ffcb;
  font-weight: 700;
}

.error-message {
  margin-top: 12px;
  color: #ffe6e6;
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
  .trainer-grid,
  .booking-panel,
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

  .booking-shell {
    padding: 24px;
    border-radius: 28px;
  }

  .trainer-card,
  .booking-panel {
    border-radius: 22px;
  }

  .trainer-image {
    min-height: 210px;
  }
}
</style>
