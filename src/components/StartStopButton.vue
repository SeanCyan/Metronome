<template>
  <button
    class="start-stop-button"
    :class="{ playing: isPlaying, pulse: shouldPulse }"
    @click="$emit('toggle')"
  >
    <span class="icon">{{ isPlaying ? '⏸' : '▶' }}</span>
  </button>
</template>

<script setup>
import { defineProps } from 'vue';

defineProps({
  isPlaying: Boolean,
  shouldPulse: Boolean // will be set to true briefly on each beat
});
</script>

<style scoped>
.start-stop-button {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: none;
  font-size: 2rem;
  background-color: #444;
  color: white;
  cursor: pointer;
  transition: box-shadow 0.2s, transform 0.1s;
  box-shadow: 0 0 0 rgba(0, 0, 0, 0.2);
  margin:70px 0;
}
.start-stop-button:hover {
background-color: #e2e2e25e;
}
.start-stop-button.pulse {
  box-shadow: 0 0 150px 0px rgba(0, 255, 136, 0.7);
}

.start-stop-button:active {
  transform: scale(0.95);
}

.icon {
  line-height: 80px;
}
@media screen and (max-width:900px) {
.start-stop-button {
  margin:50px 0 !important;
}
}
</style>