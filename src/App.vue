<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const startDate = ref(new Date('2023-12-24T10:30:00'))
const days = ref(0)
const hours = ref(0)
const minutes = ref(0)
const seconds = ref(0)
let timer = null

const calculateTimeElapsed = () => {
  const now = new Date().getTime()
  const elapsed = now - startDate.value.getTime()

  days.value = Math.floor(elapsed / (1000 * 60 * 60 * 24))
  hours.value = Math.floor((elapsed % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  minutes.value = Math.floor((elapsed % (1000 * 60 * 60)) / (1000 * 60))
  seconds.value = Math.floor((elapsed % (1000 * 60)) / 1000)
}

onMounted(() => {
  timer = setInterval(calculateTimeElapsed, 1000)
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})

// Array com todas as fotos disponíveis
const currentPhoto = ref(
  'https://raw.githubusercontent.com/vitorflopes/minha-princesa/b8f3d1f7a41ca35d3dbfd66e025a0d8d5f25719d/src/assets/1.jpg'
)
console.log(currentPhoto.value)

const changePhoto = () => {
  let newNumber
  do {
    newNumber = Math.floor(Math.random() * 15) + 1
  } while (
    `https://raw.githubusercontent.com/vitorflopes/minha-princesa/b8f3d1f7a41ca35d3dbfd66e025a0d8d5f25719d/src/assets/${newNumber}.jpg` ===
    currentPhoto.value
  )

  currentPhoto.value = `/src/assets/${newNumber}.jpg`
  console.log(currentPhoto.value)
}
</script>

<template>
  <div class="container">
    <div class="countdown">
      <div class="countdown-item">
        <span class="number">{{ days }}</span>
        <span class="label">Dias</span>
      </div>
      <div class="countdown-item">
        <span class="number">{{ hours }}</span>
        <span class="label">Horas</span>
      </div>
      <div class="countdown-item">
        <span class="number">{{ minutes }}</span>
        <span class="label">Minutos</span>
      </div>
      <div class="countdown-item">
        <span class="number">{{ seconds }}</span>
        <span class="label">Segundoss</span>
      </div>
    </div>

    <div class="photo-container">
      <img :src="currentPhoto" alt="Nosso momento especial" class="photo" />
    </div>

    <button @click="changePhoto" class="photo-button">Próxima Memória ❤️</button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  width: 100%;
  background-color: #1a1a1a;
  color: white;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.countdown {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  margin-bottom: 3rem;
}

.photo-container {
  width: 80%;
  max-width: 500px;
  margin-top: 2rem;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 0 200px #ff69b42f;
  border: 2px solid #ff69b4;
}

.photo {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.3s ease;
}

.photo:hover {
  transform: scale(1.02);
}

/* Media queries para telas menores */
@media (max-width: 768px) {
  .photo-container {
    width: 90%;
    max-width: 400px;
  }
}

@media (max-width: 375px) {
  .photo-container {
    width: 95%;
    max-width: 300px;
  }
}

.countdown-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

@keyframes pulse {
  0% {
    text-shadow: 0 0 100px #ff69b4, 0 0 80px #ff69b4;
  }
  50% {
    text-shadow: 0 0 400px #ff69b4, 0 0 200px #ff69b4;
  }
  100% {
    text-shadow: 0 0 100px #ff69b4, 0 0 80px #ff69b4;
  }
}

.number {
  font-size: 6rem;
  font-weight: bold;
  min-width: 120px;
  text-align: center;
  text-shadow: 0 0 200px #ff69b4, 0 0 100px #ff69b4;
  animation: pulse 1s infinite ease-in-out;
}

.label {
  font-size: 1.5rem;
  text-transform: uppercase;
  margin-top: 0.5rem;
}

/* Media queries para telas menores */
@media (max-width: 768px) {
  .countdown {
    gap: 1rem; /* Reduz o espaço entre os itens */
  }

  .number {
    font-size: 3rem; /* Reduz o tamanho dos números */
    min-width: 60px; /* Reduz a largura mínima */
  }

  .label {
    font-size: 0.9rem; /* Reduz o tamanho das labels */
  }
}

/* Para telas muito pequenas */
@media (max-width: 375px) {
  .countdown {
    gap: 0.5rem; /* Reduz ainda mais o espaço */
  }

  .number {
    font-size: 2rem; /* Reduz ainda mais o tamanho dos números */
    min-width: 45px;
  }

  .label {
    font-size: 0.8rem;
  }
}

.photo-button {
  margin-top: 2rem;
  padding: 1rem 2rem;
  font-size: 1.2rem;
  background-color: transparent;
  color: #ff69b4;
  border: 2px solid #ff69b4;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.photo-button:hover {
  background-color: #ff69b4;
  color: white;
  box-shadow: 0 0 20px #ff69b4;
}

@media (max-width: 768px) {
  .photo-button {
    font-size: 1rem;
    padding: 0.8rem 1.6rem;
  }
}
</style>
