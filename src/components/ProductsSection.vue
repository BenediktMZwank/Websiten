<template>
  <section id="produkte" ref="sectionRef" class="products-section">
    <div class="container">
      <div class="section-heading centered reveal" :class="{ visible }">
        <p class="section-tag">Shop</p>
        <h2>Schlaeger fuer dein Spiel</h2>
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
    </div>
  </section>
</template>

<script>
import headBoomImage from '../assets/head-boom.svg'
import headExtremeImage from '../assets/head-extreme.svg'
import headGravityImage from '../assets/head-gravity.svg'

export default {
  name: 'ProductsSection',
  data() {
    return {
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

.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
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
  .product-grid {
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

  .product-image-wrap {
    aspect-ratio: 1 / 1;
    padding: 18px;
  }
}
</style>
