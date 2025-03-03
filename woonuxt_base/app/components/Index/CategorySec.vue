<script lang="ts" setup>
// Prop-ként fogadjuk a kategóriákat a szülőtől
defineProps<{
  categories: ProductCategory[]
}>();
</script>

<template>
  <main class="container">
    <div v-if="categories?.length"
        class="grid grid-cols-2 gap-4 my-6 md:grid-cols-3 lg:gap-8 xl:grid-cols-4">
        <CategoryCard v-for="(category, i) in categories" :key="i" :node="category"
            :image-loading="i <= 2 ? 'eager' : 'lazy'" />
    </div>
  </main>
</template>