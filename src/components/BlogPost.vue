<script setup>
// defineProps(['id', 'title', 'desc']);
// const { id, title, desc } = post;
const post = defineProps({
  id: Number,
  title: String,
  desc: {
    type: String,
    default: "sem descrição"
  },
  like: Function,
});
// const emits = defineEmits(['like']);
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{id}} - {{title}}</h5>
      <p>{{desc}}</p>

      <button 
        @click="like(title)"
        class="btn btn-primary" 
      >Gosto</button>

      <!-- <button 
        @click="emits('like', title)"
        class="btn btn-primary" 
      >Gosto</button> -->
    </div>
  </div>
</template>