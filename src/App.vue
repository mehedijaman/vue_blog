<script setup>
import {ref, provide} from 'vue'
import axios from 'axios'
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Categories from './components/Categories.vue'
import Footer from './components/Footer.vue'

const categoryList = ref({});

let showModal = ref(false)
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
        Object.assign(categoryList.value, res.data)
    } catch (error) {
        console.error(error)
        return []
    }
}
fetchCategories()

provide('categories', categoryList )
provide('baseUrl', baseUrl )
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
  


    <!-- component -->
    <div v-show="showModal" class="fixed left-0 top-0 flex h-full w-full items-center justify-center bg-black bg-opacity-50 py-10">
      <div class="max-h-full w-full max-w-xl overflow-y-auto sm:rounded-2xl bg-white">
        <div class="w-full">
          <div class="m-8 my-20 max-w-[400px] mx-auto">
            <div class="mb-8">
              <h1 class="mb-4 text-3xl font-extrabold">Change Wordpress API</h1>
              <input v-model="baseUrl" type="text" class="w-full py-2 px-5 focus:outline-none border border-black rounded-2xl" placeholder="e.g. https://mehedipata.com/wp-json/wp/v2">
            </div>
            <div class="space-y-4">
              <button @click.prevent="changeAPI()" class="p-3 bg-black rounded-full text-white w-full font-semibold">Change API</button>
              <button @click="showModal=false" class="p-3 bg-white border rounded-full w-full font-semibold">Cancel</button>
            </div>
          </div>
        </div>
      </div>
    </div>

</template>