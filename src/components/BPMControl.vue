<template>
  <div class="bpm-control">
    <div>
            <button @click="decreaseBpm" class="bpm-button">–</button>
        <label for="bpm">Tempo: {{ localBpm }} BPM</label>
          <button @click="increaseBpm" class="bpm-button">+</button>
          <p class="tempo-label" :style="{ color: tempoInfo.color }">{{ tempoInfo.label }}</p>
        <input
        type="range"
        min="40"
        max="240"
        v-model="localBpm"
        class="slider"
        />
    </div>
  </div>
</template>

<script setup>
import { ref, watch, computed } from 'vue';

const props = defineProps(['bpm']);
const emit = defineEmits(['update:bpm']);

const localBpm = ref(90); // default BPM of 90

watch(localBpm, (newVal) => {
  emit('update:bpm', newVal);
});

function increaseBpm() {
  if (localBpm.value < 240) localBpm.value++;
}

function decreaseBpm() {
  if (localBpm.value > 40) localBpm.value--;
}

function getTempoInfo(bpm) {
  if (bpm < 60) return { label: 'Largo', color: '#a7fffc' };
  if (bpm < 66) return { label: 'Larghetto', color: '#3dd3ff' }; 
  if (bpm < 76) return { label: 'Adagio', color: '#3d8fff' }; 
  if (bpm < 108) return { label: 'Andante', color: '#583dff' };
  if (bpm < 120) return { label: 'Moderato', color: '#8500ff' };
  if (bpm < 168) return { label: 'Allegro', color: '#ff00e1' };
  if (bpm < 200) return { label: 'Presto', color: '#ff006c' };
  return { label: 'Prestissimo', color: '#ff0025' };      
};

const tempoInfo = computed(() => getTempoInfo(localBpm.value));
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Nova+Square&display=swap');
label {
    color:#ffffff;
    font-weight: normal;
    letter-spacing:1px;
    font-family: "Nova Square", sans-serif;
    font-size:20px;
    line-height:24px;
}
p {
    font-size:18px;
    font-style:italic;
        font-weight: normal;
    letter-spacing:1px;
    font-family: "Nova Square", sans-serif;
    margin: 0 auto;
}
input[type="range"] {
  accent-color:rgba(0, 255, 149, 0.7);
  width: 280px;
  display:block;
  margin: 20px auto;
}
.bpm-control {
  display: flex;
  justify-content: space-evenly;
  gap: 10px;
}



.bpm-button {
  font-size: 14px;
  border: none;
  background: transparent;
  color:#fff;
  cursor: pointer;
}

.bpm-button:hover {
  color: #00ffdd;
}
</style>