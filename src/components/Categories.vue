<script setup>
import { inject } from 'vue';

const categories = inject('categories')
</script>
<template>
    <ul v-for="(category, index) in categories" :key="index" class="w-48 text-sm font-medium text-gray-900 bg-white border border-gray-200 rounded-lg dark:bg-gray-700 dark:border-gray-600 dark:text-white">
        <li class="w-full px-4 py-2 border-b border-gray-200 rounded-t-lg dark:border-gray-600">
            <RouterLink :to="`posts?categories=${category.id}`">{{ category.name }} ({{ category.count }})</RouterLink>
        </li>
    </ul>
</template>