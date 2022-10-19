<script setup>
import { ref, computed, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const name = "Vue 3";
const posts = ref([]); 
const postXPage = 10;
const start = ref(0);
const end = ref(10);
const loading = ref(false);

let maxLength = computed(() => posts.value.length);

const likedPost = ref('');
const selectPost = (postTitle) => likedPost.value = postTitle;
const prevPage = () => {
  start.value -= postXPage;
  end.value -= postXPage;
};
const nextPage = () => {
  start.value = start.value + postXPage;
  end.value = end.value + postXPage;
};

const fecthData = async () => {
  loading.value = true;
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error)
  }
  loading.value = false;
} 

onMounted(async () => {
  fecthData();
})

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then(res => res.json())
//   .then(data => {
//     setTimeout(() => {
//       loading.value = false;
//     }, 2000);
//   })
//   .finally(() => loading.value = false);
</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>Ola {{ name.toUpperCase() }}</h1>
    
    <h2>Meu Post Favorito: {{likedPost}}</h2>

    <PaginatePost 
      @prev="prevPage"
      @next="nextPage"
      :start="start"
      :end="end"
      :maxLength="maxLength"
      class="mb-2"
    />

    <blog-post 
      v-for="p in posts.slice(start, end)" 
      :key="p.id"
      :id="p.id"
      :title="p.title"
      :desc="p.desc"
      :like="selectPost"
    />

    <!-- <blog-post 
      v-for="p in posts" 
      :key="p.id"
      :id="p.id"
      :title="p.title"
      :desc="p.desc"
      @like="selectPost"
    /> -->
  </div>
</template>