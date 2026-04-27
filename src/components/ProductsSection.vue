<template>
  <section id="produkte" ref="sectionRef" class="products-section">
    <div class="container">
      <div class="section-heading centered reveal" :class="{ visible }">
        <p class="section-tag">Shop</p>
        <h2>Schlaeger fuer dein Spiel</h2>
        <p>
          Such dir deinen Schlaeger aus und schick uns deine Bestellung direkt online.
        </p>
      </div>

      <div class="product-grid">
        <article
          v-for="(product, index) in products"
          :key="product.name"
          class="product-card reveal"
          :class="[`reveal-delay-${index + 1}`, { visible }]"
        >
          <div class="product-image-wrap">
            <img :src="product.image" :alt="product.name" class="product-image" />
          </div>
          <div class="product-info">
            <h3>{{ product.name }}</h3>
            <p>{{ product.price }}</p>
          </div>
        </article>
      </div>

      <div class="shop-panel reveal reveal-delay-2" :class="{ visible }">
        <div class="panel-copy">
          <p class="section-tag small">Schlaeger bestellen</p>
          <h3>Bestellung auf Rechnung anfragen</h3>
          <p>
            Waehle dein Modell aus und trage alle Versanddaten ein. Die Bestellung
            wird dann ueber EmailJS an euch weitergeleitet.
          </p>
          <div class="billing-note">
            <span class="billing-badge">Zahlung</span>
            <p>
              Du bestellst auf Rechnung. Nach deiner Anfrage melden wir uns mit
              den finalen Bestelldetails und der Rechnung bei dir.
            </p>
          </div>
        </div>

        <form ref="orderForm" class="shop-form" @submit.prevent="submitOrder">
          <div class="form-group">
            <label for="product">Schlaeger</label>
            <select id="product" v-model="order.product" name="product" required>
              <option disabled value="">Bitte Schlaeger auswaehlen</option>
              <option v-for="product in products" :key="product.name" :value="product.name">
                {{ product.name }} - {{ product.price }}
              </option>
            </select>
          </div>

          <div class="form-group">
            <label for="quantity">Anzahl</label>
            <input id="quantity" v-model="order.quantity" name="quantity" type="number" min="1" placeholder="1" required />
          </div>

          <div class="form-group">
            <label for="customer-name">Name</label>
            <input id="customer-name" v-model="order.name" name="name" type="text" placeholder="Vor- und Nachname" required />
          </div>

          <div class="form-group">
            <label for="customer-email">E-Mail</label>
            <input
              id="customer-email"
              v-model="order.email"
              name="email"
              type="email"
              placeholder="deinname@mail.de"
              required
            />
          </div>

          <div class="form-group">
            <label for="customer-phone">Telefonnummer</label>
            <input
              id="customer-phone"
              v-model="order.phone"
              name="phone"
              type="tel"
              placeholder="+49 123 456789"
              required
            />
          </div>

          <div class="form-group full-width">
            <label for="street">Strasse und Hausnummer</label>
            <input
              id="street"
              v-model="order.street"
              name="street"
              type="text"
              placeholder="Musterstrasse 12"
              required
            />
          </div>

          <div class="form-group">
            <label for="postal-code">Postleitzahl</label>
            <input id="postal-code" v-model="order.postalCode" name="postal_code" type="text" placeholder="12345" required />
          </div>

          <div class="form-group">
            <label for="city">Ort</label>
            <input id="city" v-model="order.city" name="city" type="text" placeholder="Berlin" required />
          </div>

          <div class="form-group">
            <label for="country">Land</label>
            <input id="country" v-model="order.country" name="country" type="text" placeholder="Deutschland" required />
          </div>

          <div class="form-group full-width">
            <label for="order-message">Nachricht</label>
            <textarea
              id="order-message"
              v-model="order.message"
              name="message"
              rows="4"
              placeholder="Optional: Besaitung, Griffstaerke oder weitere Hinweise"
            ></textarea>
          </div>

          <input type="hidden" name="site_name" value="MegoPlayTennis Shop" />
          <input type="hidden" name="request_type" value="Schlaegerbestellung" />

          <button type="submit" class="btn btn-primary full-button magnetic-button" :disabled="isSubmittingOrder">
            {{ isSubmittingOrder ? 'Bestellung wird gesendet...' : 'Schlaeger bestellen' }}
          </button>
        </form>
      </div>

      <p v-if="orderSubmitted" class="success-message reveal visible">
        Danke! Die Bestellung wurde uebermittelt.
      </p>

      <p v-if="orderErrorMessage" class="error-message reveal visible">
        {{ orderErrorMessage }}
      </p>
    </div>
  </section>
</template>

<script>
import emailjs from '@emailjs/browser'
import headBoomImage from '../assets/head-boom.jpg'
import headExtremeImage from '../assets/head-extreme.jpg'
import headGravityImage from '../assets/head-gravity.jpg'

export default {
  name: 'ProductsSection',
  data() {
    return {
      isSubmittingOrder: false,
      orderSubmitted: false,
      orderErrorMessage: '',
      visible: false,
      observer: null,
      products: [
        {
          name: 'Head Boom',
          price: '140 EUR',
          image: headBoomImage,
        },
        {
          name: 'Head Gravity',
          price: '190 EUR',
          image: headGravityImage,
        },
        {
          name: 'Head Extreme',
          price: '190 EUR',
          image: headExtremeImage,
        },
      ],
      order: {
        product: '',
        quantity: '1',
        name: '',
        email: '',
        phone: '',
        street: '',
        postalCode: '',
        city: '',
        country: '',
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
    resetOrderForm() {
      this.order = {
        product: '',
        quantity: '1',
        name: '',
        email: '',
        phone: '',
        street: '',
        postalCode: '',
        city: '',
        country: '',
        message: '',
      }
    },
    async submitOrder() {
      this.orderErrorMessage = ''
      this.orderSubmitted = false

      const serviceId = import.meta.env.VITE_EMAILJS_SERVICE_ID
      const templateId = import.meta.env.VITE_EMAILJS_SHOP_TEMPLATE_ID || import.meta.env.VITE_EMAILJS_TEMPLATE_ID
      const publicKey = import.meta.env.VITE_EMAILJS_PUBLIC_KEY

      if (!serviceId || !templateId || !publicKey) {
        this.orderErrorMessage = 'EmailJS ist noch nicht fertig konfiguriert. Bitte trage die Env-Werte ein.'
        return
      }

      if (!this.$refs.orderForm) {
        this.orderErrorMessage = 'Das Bestellformular konnte nicht gefunden werden.'
        return
      }

      try {
        this.isSubmittingOrder = true

        await emailjs.sendForm(serviceId, templateId, this.$refs.orderForm, {
          publicKey,
        })

        this.orderSubmitted = true
        this.resetOrderForm()
      } catch (error) {
        console.error('EmailJS Versand fuer Bestellung fehlgeschlagen:', error)
        this.orderErrorMessage = 'Die Bestellung konnte gerade nicht gesendet werden. Bitte versuche es erneut.'
      } finally {
        this.isSubmittingOrder = false
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

.products-section {
  padding: 96px 0;
  position: relative;
  z-index: 2;
  background: rgba(248, 255, 249, 0.88);
  border-top: 1px solid rgba(86, 164, 108, 0.12);
  border-bottom: 1px solid rgba(86, 164, 108, 0.12);
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
  color: #153824;
}

.section-heading p {
  margin: 14px auto 0;
  max-width: 680px;
  color: rgba(21, 56, 36, 0.78);
  line-height: 1.8;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
  margin-bottom: 30px;
}

.product-card {
  overflow: hidden;
  border-radius: 8px;
  border: 1px solid rgba(108, 181, 128, 0.18);
  background: rgba(255, 255, 255, 0.88);
  box-shadow: 0 18px 60px rgba(65, 106, 72, 0.12);
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

.product-card:hover {
  transform: translateY(-8px);
  border-color: rgba(43, 157, 94, 0.26);
  box-shadow: 0 24px 70px rgba(65, 106, 72, 0.16);
}

.product-image-wrap {
  display: grid;
  place-items: center;
  aspect-ratio: 1 / 1.05;
  padding: 24px;
  background: #ffffff;
}

.product-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.product-info {
  padding: 22px 24px 24px;
  border-top: 1px solid rgba(108, 181, 128, 0.12);
}

.product-info h3 {
  margin: 0 0 8px;
  color: #153824;
  font-size: 1.45rem;
}

.product-info p {
  margin: 0;
  color: #2b9d5e;
  font-size: 1.5rem;
  font-weight: 800;
}

.shop-panel {
  display: grid;
  grid-template-columns: 0.82fr 1.18fr;
  gap: 24px;
  padding: 28px;
  align-items: start;
  border-radius: 36px;
  border: 1px solid rgba(108, 181, 128, 0.18);
  background:
    radial-gradient(circle at top right, rgba(255, 229, 153, 0.46), transparent 26%),
    radial-gradient(circle at bottom left, rgba(172, 224, 194, 0.36), transparent 28%),
    linear-gradient(145deg, rgba(255, 252, 244, 0.98), rgba(243, 250, 245, 0.98));
  box-shadow: 0 24px 70px rgba(26, 58, 37, 0.12);
}

.panel-copy {
  padding: 10px 6px 10px 0;
  color: #153824;
}

.panel-copy h3 {
  margin: 0 0 10px;
  font-size: 1.8rem;
  color: #153824;
}

.panel-copy p:last-child {
  margin: 0 0 20px;
  line-height: 1.8;
  color: rgba(21, 56, 36, 0.8);
}

.section-tag.small {
  margin-bottom: 10px;
  font-size: 0.72rem;
  color: #2b9d5e;
}

.billing-note {
  padding: 20px;
  border-radius: 24px;
  border: 1px solid rgba(43, 157, 94, 0.18);
  background: rgba(255, 255, 255, 0.72);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.7);
}

.billing-badge {
  display: inline-flex;
  align-items: center;
  padding: 6px 12px;
  margin-bottom: 12px;
  border-radius: 999px;
  background: #153824;
  color: #f8fff9;
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.billing-note p {
  margin: 0;
  color: rgba(21, 56, 36, 0.86);
  line-height: 1.7;
}

.shop-form {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
  padding: 24px;
  border-radius: 28px;
  border: 1px solid rgba(43, 157, 94, 0.16);
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.82), rgba(248, 255, 250, 0.94)),
    linear-gradient(135deg, rgba(255, 255, 255, 0.22), rgba(255, 255, 255, 0));
  box-shadow: 0 16px 40px rgba(21, 56, 36, 0.08);
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  margin-bottom: 8px;
  font-weight: 600;
  color: #153824;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  padding: 14px 16px;
  border-radius: 16px;
  border: 1px solid rgba(43, 157, 94, 0.16);
  background: rgba(255, 255, 255, 0.9);
  color: #153824;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.25s ease, box-shadow 0.25s ease, transform 0.25s ease;
}

.form-group select {
  appearance: none;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(21, 56, 36, 0.46);
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  border-color: rgba(43, 157, 94, 0.5);
  box-shadow: 0 0 0 4px rgba(43, 157, 94, 0.12);
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
  background: linear-gradient(135deg, #153824, #2b9d5e);
  color: #f8fff9;
  box-shadow: 0 12px 30px rgba(21, 56, 36, 0.18);
}

.btn-primary:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 18px 36px rgba(21, 56, 36, 0.24);
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
  color: #1f7a42;
  font-weight: 700;
}

.error-message {
  margin-top: 12px;
  color: #b42318;
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

.reveal-delay-3 {
  transition-delay: 0.26s;
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
  .product-grid,
  .shop-panel,
  .shop-form {
    grid-template-columns: 1fr;
  }

  .product-image-wrap {
    aspect-ratio: 1 / 0.78;
  }
}

@media (max-width: 640px) {
  .container {
    width: min(100% - 28px, 1200px);
  }

  .products-section {
    padding: 72px 0;
  }

  .shop-panel {
    padding: 22px;
    border-radius: 24px;
  }

  .shop-form {
    padding: 20px;
    border-radius: 22px;
  }

  .product-image-wrap {
    aspect-ratio: 1 / 1;
    padding: 18px;
  }
}
</style>
