<script setup>
const props = defineProps(['start', 'end', 'maxLength']);
const emits = defineEmits(['next', 'prev']);

const goNext = () => {
  emits('next');
  console.log('go to the next page');
}
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button 
      @click="emits('prev')"
      :disabled="start <= 0"
      class="btn btn-outline-primary"
    >prev</button>

    <button 
      @click="goNext"
      :disabled="end === maxLength"
      class="btn btn-primary"
    >next</button>
  </div>
</template>