<template>
  <div class="tech-app">
    <header>
      <h1>🚀 Daftar Kegiatan Teknologi</h1>
      
      <p>Centang jika selesai, klik nama kegiatan untuk melihat penjelasan.</p>

      <h3>233510308 - TOGI MARITO MANURUNG</h3>
    </header>

    <div class="tech-grid">
      <div
        v-for="(tech, index) in filteredTechnologies"
        :key="index"
        class="tech-pion"
        :class="{ completed: tech.completed }"
      >
        <div class="checkbox-wrapper">
          <input type="checkbox" v-model="tech.completed" />
        </div>
        <h3 @click="selectTech(tech)" class="clickable">{{ tech.name }}</h3>
        <button class="delete-btn" @click="removeTech(index)">🗑</button>
      </div>
    </div>

    <div class="controls">
      <button @click="resetAll" class="reset-btn">🔄 Reset Semua</button>
      <label>
        <input type="checkbox" v-model="showIncompleteOnly" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <div v-if="selectedTech" class="tech-info">
      <h2>{{ selectedTech.name }}</h2>
      <p><strong>Pengertian:</strong> {{ selectedTech.description }}</p>
      <p><strong>Pembelajaran:</strong> {{ selectedTech.learning }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const showIncompleteOnly = ref(false)
const selectedTech = ref(null)

const technologies = ref([
  {
    name: 'Kecerdasan Buatan',
    completed: false,
    description: 'Simulasi proses berpikir manusia oleh komputer.',
    learning: 'Pelajari dasar-dasar AI seperti machine learning dan neural networks.'
  },
  {
    name: 'Blockchain',
    completed: false,
    description: 'Sistem pencatatan digital yang aman dan transparan.',
    learning: 'Pelajari cara kerja blockchain, smart contract, dan crypto.'
  },
  {
    name: '5G',
    completed: false,
    description: 'Jaringan generasi kelima untuk koneksi lebih cepat dari generasi-generasi sebelumnya.',
    learning: 'Pelajari teknologi jaringan seluler dan dampaknya pada IoT.'
  },
  {
    name: 'Internet of Things (IoT)',
    completed: false,
    description: 'Koneksi perangkat fisik ke internet.',
    learning: 'Pelajari sensor, mikrokontroler, dan komunikasi antar perangkat.'
  },
  {
    name: 'Realitas Virtual (VR)',
    completed: false,
    description: 'Pengalaman digital imersif melalui headset.',
    learning: 'Pelajari Unity, Unreal Engine, dan desain pengalaman virtual.'
  },
  {
    name: 'Cloud Computing',
    completed: false,
    description: 'Pemrosesan dan penyimpanan data di internet.',
    learning: 'Pelajari AWS, Azure, dan Google Cloud.'
  },
  {
    name: 'Big Data',
    completed: false,
    description: 'Analisis volume data besar untuk mengambil keputusan.',
    learning: 'Pelajari Hadoop, Spark, dan dasar-dasar data analytics.'
  }
  // Tambahkan data lainnya jika perlu
])

const filteredTechnologies = computed(() =>
  showIncompleteOnly.value
    ? technologies.value.filter(tech => !tech.completed)
    : technologies.value
)

function removeTech(index) {
  technologies.value.splice(index, 1)
  if (selectedTech.value === technologies.value[index]) {
    selectedTech.value = null
  }
}

function resetAll() {
  technologies.value.forEach(tech => (tech.completed = false))
  selectedTech.value = null
}

function selectTech(tech) {
  selectedTech.value = tech
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap');

.tech-app {
  background: radial-gradient(ellipse at bottom, #000000 0%, #2e1f47 100%);
  color: white;
  padding: 2rem;
  text-align: center;
  min-height: 100vh;
  font-family: 'Orbitron', sans-serif;
  overflow: hidden;
  position: relative;
}

header h1 {
  font-size: 2.5rem;
  color: #fffa00;
  margin-bottom: 1rem;
  text-shadow: 0 0 15px #fffa00, 0 0 30px #fffa00;
}

header p {
  color: #b0eaff;
  font-size: 1.1rem;
  margin-top: 0;
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.7);
}

.tech-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
  margin-top: 2rem;
  position: relative;
  z-index: 1;
}

.tech-pion {
  background-color: rgba(0, 0, 0, 0.6);
  padding: 1.5rem;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
  position: relative;
}

.tech-pion.completed {
  opacity: 0.5;
  text-decoration: line-through;
}

.checkbox-wrapper {
  position: absolute;
  top: 10px;
  left: 10px;
}

.delete-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: transparent;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  color: #ff6666;
  transition: transform 0.2s;
}

.delete-btn:hover {
  transform: scale(1.2);
}

.clickable {
  cursor: pointer;
  transition: color 0.3s;
}

.clickable:hover {
  color: #00ffff;
}

.controls {
  margin-top: 2rem;
  text-align: center;
}

.reset-btn {
  background-color: #a59e85;
  border: none;
  padding: 0.6rem 1rem;
  border-radius: 10px;
  font-size: 1rem;
  cursor: pointer;
  margin-bottom: 1rem;
  transition: background-color 0.3s ease;
}

.reset-btn:hover {
  background-color: #ffe066;
}

.tech-info {
  background-color: rgba(0, 0, 0, 0.8);
  padding: 2rem;
  margin-top: 3rem;
  text-align: left;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0, 255, 255, 0.4);
}

.tech-info h2 {
  font-size: 2rem;
  color: #fffa00;
}

.tech-info p {
  font-size: 1.1rem;
  color: #b0eaff;
  line-height: 1.6;
}

@media (max-width: 768px) {
  .tech-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .tech-grid {
    grid-template-columns: 1fr;
  }
}
</style>