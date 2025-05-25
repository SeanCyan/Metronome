<script setup>
import { ref, watch, onUnmounted } from 'vue';
import { watchEffect } from 'vue';
import { defineEmits } from 'vue';

const props = defineProps({
  bpm: Number,
  isPlaying: Boolean,
  beatsPerMeasure: Number,
  soundSet: {
    type: String,
    default: 'default'
  }
});

const currentBeat = ref(0);
const tickAudio = ref(new Audio());
const accentAudio = ref(new Audio());

watchEffect(() => {
  tickAudio.value = new Audio(`/${props.soundSet}_tick.wav`);
  accentAudio.value = new Audio(`/${props.soundSet}_accent.wav`);
});

let intervalId = null;

const emit = defineEmits(['beat']);

function playClick(beat) {
  const shouldAccent = (props.beatsPerMeasure === 6)
    ? beat === 0 || beat === 3
    : beat === 0;

  const audio = shouldAccent ? accentAudio.value : tickAudio.value;
  audio.currentTime = 0;
  audio.play();
  emit('beat'); // right after playing the sound
}

function start() {
  stop();
  const interval = (60 / props.bpm) * 1000;
  intervalId = setInterval(() => {
    playClick(currentBeat.value);
    currentBeat.value = (currentBeat.value + 1) % props.beatsPerMeasure;
  }, interval);
}

function stop() {
  clearInterval(intervalId);
  intervalId = null;
  currentBeat.value = 0;
}

watch(() => props.isPlaying, (playing) => {
  if (playing) start();
  else stop();
});

watch(() => props.bpm, () => {
  if (props.isPlaying) start();
});

onUnmounted(stop);
</script>