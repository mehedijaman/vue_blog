<script setup>
import {ref} from 'vue'
import axios from 'axios'
import { RouterLink } from 'vue-router'
import PreLoader from '../components/PreLoader.vue'
import PostCard from '../components/PostCard.vue'

let isLoading = ref(true)
const posts = ref({})
let baseUrl = ref(localStorage.getItem('baseUrl'))

async function fetchPosts(){
  try {
    const url = `${baseUrl.value}/posts`
    const res = await axios.get(url)
    Object.assign(posts.value,res.data)
    isLoading.value = false
    // getFaturedImage(res.data)

  } catch (error) {
    console.log(error)
    return []
  }
}

// async function getFaturedImage(posts){
//   for(const post of posts){
//     if(post.featured_media != 0){
//       const url = `${baseUrl.value}/media/${post.featured_media}`
//       const res = await axios.get(url)
//       const data = [
//         post,
//         res.data
//       ]
//       postList.push(data)
//     }
//     else{
//       const data = []
//       postList.push(data)
//     }    
//   }
// }

fetchPosts()

</script>

<template>
  <div class="p-5 text-center bg-gray-100 mb-5 text-red-800 rounded-md" >
    <span class="font-bold">WPVuer</span> is a simple app built with Vue JS and Tailwind CSS that displays posts from a WordPress REST API endpoint. <br> Made with Passion by <a href="https://linkedin.com/in/mehedijaman" target="_blank" class="text-blue-900">Mehedi Jaman</a>. Get the Source code from <a href="https//github.com/mehedijaman/wvuer.git" target="_blank" class="text-blue-900">Github</a>
  </div>

  <PreLoader v-if="isLoading"></PreLoader>
  <PostCard v-for="(post, index) in posts" :key="index" :post="post"></PostCard>
</template>
