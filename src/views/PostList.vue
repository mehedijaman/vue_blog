<script setup>
import {reactive,ref, watch} from 'vue'
import axios from 'axios'
import { useRoute } from 'vue-router'
import PostCardVue from '../components/PostCard.vue'

const baseUrl = ref(localStorage.getItem('baseUrl'))

const route = useRoute()
const posts = ref({})
let isLoading = ref(true)

async function filterPost(){
  try { 
    const categoryId = route.query.categories
    const url = `${baseUrl.value}/posts?categories=${categoryId}`
    const res = await axios.get(url)
    Object.assign(posts.value,res.data)
    isLoading.value = false
    console.log(posts.value)

  } catch (error) {
    console.log(error)
  }
}


// filterPost()
// watch(() => route.query.categories, filterPost)
</script>

<template>
  <PostCard v-for="(post, index) in posts" :key="index" :post="post"></PostCard>
</template>