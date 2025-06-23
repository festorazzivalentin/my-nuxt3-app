<script setup>
import { ref, watch } from 'vue';
const { data: apod, error } = await useFetch('https://api.nasa.gov/planetary/apod?api_key=alsel4xFJg4x6CFVy7aGgRDErx0eCW1K0WXBcLNl&count=1');

const currentIndex = ref(0);
const zoomed = ref(false);
const showExplanation = ref(false);

function reloadPage() {
  window.location.reload();
}

function toggleZoom() {
  zoomed.value = !zoomed.value;
}

function toggleExplanation() {
  showExplanation.value = !showExplanation.value;
}

// Reset index if data changes
watch(apod, () => { currentIndex.value = 0; });
</script>
<template>
  <div class="nasa-api-main">
    <div class="nasa-api-card">
      <h1 class="nasa-title">NASA Astronomy Picture of the Day</h1>
      <div v-if="error" class="error-msg">Error: {{ error.message }}</div>
      <div v-else-if="apod && apod.length">
        <div class="nasa-img-container">
          <img
            :src="apod[currentIndex]?.hdurl || apod[currentIndex]?.url"
            :alt="apod[currentIndex]?.title"
            class="nasa-img"
            :class="{ zoomed: zoomed }"
            @click="toggleZoom"
            @touchstart.prevent="toggleZoom"
            title="Haz clic o toca para hacer zoom"
          />
        </div>
        <h2 class="nasa-img-title">{{ apod[currentIndex]?.title }}</h2>
        <transition name="fade-slide">
          <div v-if="showExplanation">
            <p class="nasa-img-explanation">{{ apod[currentIndex]?.explanation }}</p>
            <button class="explanation-btn" @click="toggleExplanation">Ocultar</button>
          </div>
        </transition>
        <button v-if="!showExplanation" class="explanation-btn" @click="toggleExplanation">Explicación</button>
        <button class="random-btn" @click="reloadPage">Siguiente</button>
      </div>
      <div v-else class="loading-msg">Cargando imágenes</div>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&family=Quicksand:wght@400;700&display=swap');

.nasa-api-main {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #e0e7ef 0%, #f8fafc 100%);
  padding: 2rem 0;
  font-family: 'Quicksand', 'Montserrat', 'Segoe UI', Arial, sans-serif;
}
.nasa-api-card {
  background: #fff;
  border-radius: 2rem;
  box-shadow: 0 2px 24px 0 rgba(58,134,255,0.10);
  padding: 2.5rem 1.5rem 2rem 1.5rem;
  max-width: 420px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
}
.nasa-title {
  color: #3a86ff;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  text-align: center;
  font-weight: 700;
  letter-spacing: 1px;
}
.nasa-img-container {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 1.2rem;
  position: relative;
}
.nasa-img {
  max-width: 100%;
  max-height: 320px;
  width: auto;
  height: auto;
  border-radius: 1rem;
  object-fit: contain;
  background: #e0e7ef;
  box-shadow: 0 2px 12px 0 rgba(58,134,255,0.08);
  cursor: zoom-in;
  transition: all 0.6s cubic-bezier(0.22, 1, 0.36, 1);
  font-family: inherit;
  position: relative;
  z-index: 1;
}
.nasa-img.zoomed {
  position: fixed;
  inset: 0;
  margin: auto;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 9999;
  max-width: 95vw;
  max-height: 90vh;
  width: auto;
  height: auto;
  transform: scale(1.2);
  box-shadow: 0 8px 32px 0 rgba(58,134,255,0.25);
  cursor: zoom-out;
  background: #fff;
  border-radius: 1.5rem;
}
.nasa-img-title {
  font-size: 1.3rem;
  color: #22223b;
  margin: 0.5rem 0 0.5rem 0;
  text-align: center;
  font-weight: 700;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
}
.nasa-img-explanation {
  font-size: 1.08rem;
  color: #444;
  margin-bottom: 1.5rem;
  text-align: justify;
  font-family: 'Quicksand', 'Montserrat', 'Segoe UI', Arial, sans-serif;
}
.random-btn {
  background: #3a86ff;
  color: #fff;
  border: none;
  border-radius: 2rem;
  padding: 0.7rem 2.2rem;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 2px 8px 0 rgba(58,134,255,0.10);
  transition: background 0.2s, transform 0.1s;
  display: block;
  margin: 0 auto 0.5rem auto;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
}
.random-btn:hover {
  background: #265dbe;
  transform: scale(1.04);
}

.error-msg {
  color: #e63946;
  margin-top: 1.5rem;
  text-align: center;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
}
.loading-msg {
  color: #3a86ff;
  text-align: center;
  margin-top: 2rem;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
}
.explanation-btn {
  background: #fff;
  color: #3a86ff;
  border: 2px solid #3a86ff;
  border-radius: 2rem;
  padding: 0.5rem 1.5rem;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  margin: 0.5rem auto 1rem auto;
  display: block;
  transition: background 0.2s, color 0.2s;
  font-family: 'Montserrat', 'Quicksand', 'Segoe UI', Arial, sans-serif;
}
.explanation-btn:hover {
  background: #3a86ff;
  color: #fff;
}
.fade-slide-enter-active, .fade-slide-leave-active {
  transition: opacity 0.4s, transform 0.4s;
}
.fade-slide-enter-from, .fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
.fade-slide-enter-to, .fade-slide-leave-from {
  opacity: 1;
  transform: translateY(0);
}
@media (max-width: 600px) {
  .nasa-api-card {
    padding: 1.2rem 0.5rem 1.2rem 0.5rem;
    max-width: 98vw;
  }
  .nasa-img {
    max-height: 180px;
  }
  .nasa-img.zoomed {
    max-width: 100vw;
    max-height: 100vh;
    border-radius: 0.5rem;
  }
}
</style>