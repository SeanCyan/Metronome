<template>
  <div class="bpm-control">
    <label for="bpm-slider">Tempo: {{ modelValue }} BPM</label>
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
defineProps(['modelValue']);
defineEmits(['update:modelValue']);
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Nova+Square&display=swap');
label {
    color:#ffffff;
    font-weight: normal;
    letter-spacing:1px;
    font-family: "Nova Square", sans-serif;
    font-size:20px;
}
input[type="range"] {
  accent-color:rgba(0, 255, 149, 0.7);
  width: 280px;
  display:block;
  margin: 20px auto;
}
</style>