<script setup>
import {ref, provide} from 'vue'
import axios from 'axios'
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Categories from './components/Categories.vue'
import Footer from './components/Footer.vue'

const categoryList = ref({});

let baseUrl = ref(localStorage.getItem('baseUrl'))

if(baseUrl.value == null || baseUrl.value == ''){
  localStorage.setItem('baseUrl', 'https://mehedipata.com/wp-json/wp/v2')
  baseUrl.value = localStorage.getItem('baseUrl')
}

function changeAPI(){
  localStorage.setItem('baseUrl', baseUrl.value)
  showModal.value = false
  fetchCategories()
}

async function fetchCategories(){
    try {
        const url = `${baseUrl.value}/categories`
        const res = await axios.get(url)
        categoryList.value = res.data
    } catch (error) {
        console.error(error)
    }
}
fetchCategories()

provide('categories', categoryList)
provide('baseUrl', baseUrl)
</script>

<template>
  <Header></Header>
  <div class="grid grid-cols-12">
    <div class="col-span-9 p-10 mt-10 ">
      <RouterView />
    </div>
    <div class="col-span-3 pt-10 mt-10">
      <Categories></Categories>
    </div>
  </div>
  <Footer></Footer>
  




</template>