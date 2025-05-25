<template>
  <div class="bpm-control">
    <label for="bpm-slider">Tempo: {{ modelValue }} BPM<br><span class="tempo-label" :style="{ color: tempoInfo.color }">{{ tempoInfo.label }}</span></label>
    <input
      id="bpm-slider"
      type="range"
      :min="40"
      :max="240"
      :value="modelValue"
      @input="$emit('update:modelValue', +$event.target.value)"
    />
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps(['modelValue']);

const tempoInfo = computed(() => {
  const bpm = props.modelValue;
  if (bpm < 60) return { label: 'Largo', color: '#a7fffc' };
  if (bpm < 66) return { label: 'Larghetto', color: '#3dd3ff' }; 
  if (bpm < 76) return { label: 'Adagio', color: '#3d8fff' }; 
  if (bpm < 108) return { label: 'Andante', color: '#583dff' };
  if (bpm < 120) return { label: 'Moderato', color: '#8500ff' };
  if (bpm < 168) return { label: 'Allegro', color: '#ff00e1' };
  if (bpm < 200) return { label: 'Presto', color: '#ff006c' };
  return { label: 'Prestissimo', color: '#ff0025' };      
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Nova+Square&display=swap');
label {
    color:#ffffff;
    font-weight: normal;
    letter-spacing:1px;
    font-family: "Nova Square", sans-serif;
    font-size:20px;
    line-height:30px;
}
label span {
    font-size:18px;
    font-style:italic;
}
input[type="range"] {
  accent-color:rgba(0, 255, 149, 0.7);
  width: 280px;
  display:block;
  margin: 20px auto;
}
</style>