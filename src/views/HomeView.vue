<script>
import { onMounted, ref } from 'vue';

export default {
  
  setup() {
    const posts = ref([]);
    const error = ref(null);

    const load = async () => {

      try {
      let data = await fetch('http://localhost:8000/api/games')
        if (!data.ok) {
          throw Error('no data available')
        }

        posts.value = await data.json()
        console.log(posts.value)
      }
      catch (err) {
        error.value = err.message
        console.log(error.value)
      }

  }
    
  
  load();

    return { posts }
  }
}




  
</script>

<template>
  <div v-for="post in posts">
    <div>{{ post.name }}</div>
  </div>
</template>
