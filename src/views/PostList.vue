<script setup>
import {reactive,ref, watch} from 'vue'
import axios from 'axios'
import { useRoute } from 'vue-router';
import {
  Timeline, TimelineItem, TimelinePoint, TimelineTime, TimelineContent, TimelineTitle,
  Button
} from 'flowbite-vue'

const baseUrl = ref(localStorage.getItem('baseUrl'))

const route = useRoute()
const posts = reactive({})

async function fetchPosts(){
  try { 
    const categoryId = route.query.categories
    const url = `${baseUrl.value}/posts?categories=${categoryId}` 
    const res = await axios.get(url)     
    Object.assign(posts,res.data)

  } catch (error) {
    console.log(error)
  }
}

fetchPosts()
watch(() => route.query.categories, fetchPosts);
</script>

<template>
  <Timeline>
    <timeline-item v-for="(post, index) in posts" :key="index" class="bg-gray-50 p-5  rounded-md">
      <timeline-point>
        <svg aria-hidden="true" class="w-3 h-3 text-blue-600 dark:text-blue-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z" clip-rule="evenodd"></path></svg>
      </timeline-point>
      <timeline-content class="flex flex-col gap-4">
        <timeline-time>
          Posted on {{ post.date }} by MehediJaman
        </timeline-time>
        <timeline-title class="text-2xl">
          {{ post.title.rendered }}
        </timeline-title>
        <timeline-body>
          <div class="flex flex-col gap-10">
            <img class="h-96" src="https://images.unsplash.com/photo-1682687982046-e5e46906bc6e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80" alt="">
            <div v-html="post.excerpt.rendered"></div>
          </div>

        </timeline-body>
        <timeline-footer>
          <RouterLink :to="`post-details?id=${post.id}`" color="blue">
            <div class="flex items-center">
              বিস্তারিত পড়ুন
              <svg class="ml-2 -mr-1 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
            </div>
          </RouterLink>
        </timeline-footer>
      </timeline-content>
    </timeline-item>

  </Timeline>
</template>