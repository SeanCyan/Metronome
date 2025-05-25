<template>
  <div class="app">
    <h1>Metronome</h1>
    <StartStopButton
      :isPlaying="isPlaying"
      :shouldPulse="shouldPulse"
      @toggle="toggleMetronome"
    />
    <BPMControl v-model="bpm" />
    <Metronome
      :bpm="bpm"
      :isPlaying="isPlaying"
      :beatsPerMeasure="beatsPerMeasure"
      :soundSet="soundSet"
      @beat="triggerPulse"
    />
    <select v-model="selectedTimeSignature" @change="updateTimeSignature">
      <option value="4/4">4/4</option>
      <option value="2/4">2/4</option>
      <option value="3/4">3/4</option>
      <option value="6/8">6/8</option>
    </select>
    <select v-model="soundSet">
      <option value="default">Default</option>
      <option value="cowbell">Cowbell</option>
      <option value="synth">Synth</option>
      <option value="weird">Weird</option>
      <option value="tamberine">Tamberine</option>
    </select>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import BPMControl from './components/BPMControl.vue';
import StartStopButton from './components/StartStopButton.vue';
import Metronome from './components/Metronome.vue';

const bpm = ref(90);
const isPlaying = ref(false);
const selectedTimeSignature = ref('4/4');
const beatsPerMeasure = ref(4);
const beatSubdivision = ref(1); // 1 = simple (4/4, 3/4), 3 = compound (6/8)
const soundSet = ref('default');
const shouldPulse = ref(false);

function toggleMetronome() {
  isPlaying.value = !isPlaying.value;
}

function triggerPulse() {
  shouldPulse.value = true;
  setTimeout(() => shouldPulse.value = false, 100); // remove pulse after short delay
}

function updateTimeSignature() {
  switch (selectedTimeSignature.value) {
    case '3/4':
      beatsPerMeasure.value = 3;
      beatSubdivision.value = 1;
      break;
    case '6/8':
      beatsPerMeasure.value = 6;
      beatSubdivision.value = 3;
      break;
    case '2/4':
      beatsPerMeasure.value = 2;
      beatSubdivision.value = 1;
      break;
    case '4/4':
    default:
      beatsPerMeasure.value = 4;
      beatSubdivision.value = 1;
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Megrim&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Nova+Square&display=swap');
body {
  font-family: sans-serif;
  text-align: center;
  padding: 2rem;
}
button {
  padding: 0.5rem 1rem;
  margin-top: 1rem;
}
* {
  box-sizing: border-box;
}
.app {
  width:100%;
  max-width: 500px;
  margin: 0 auto;
  padding: 1rem;
}
h1 {
  color:rgb(0, 255, 157);
    font-family: "Megrim", system-ui;
  font-weight: normal;
  letter-spacing: 0.2em;
  font-size:40px;
}
button {
  font-size: 16px;
  padding: 0.6rem 1.2rem;
  margin: 0.5rem 0;
  border-radius: 8px;
}
select {
  width:200px;
  margin: 10px 20px;
  background-color:#5e5e5e;
  color:#ffffff;
  font-family: "Nova Square", sans-serif;
  border-radius: 8px;
  padding: 0.6rem 0.8rem;
  font-size:16px;
}

</style>