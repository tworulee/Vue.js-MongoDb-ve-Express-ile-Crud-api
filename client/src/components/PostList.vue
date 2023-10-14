<template>
<div class="container">
    <div v-for="post in posts" :key="post._id" class="card my-5">
  <div class="card-content">
    <div class="media"> 
      <div class="media-content">
        <p class="title is-4">{{ post.title }}</p>
      </div>
    </div>

    <div class="content">
     {{ post.content }}
      <br/>
      <strong>{{ post.creator }}</strong>
    </div>
  </div>
</div>
</div>
</template>

<script>
import { ref,onMounted } from 'vue';


export default {
    setup(){
        const posts = ref([])
        const API_URL = "http://localhost:5000/posts"

        onMounted(() => {
            getPosts()
        })

        async function getPosts() {
           try {
             const response = await fetch(API_URL)
             const json = await response.json();
             posts.value = json
           } catch (error) {
            console.log(error);
           }
        }
        return {
            posts
        }
    }
}
</script>

<style>

</style>