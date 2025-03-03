<script lang="ts" setup>
import { computed, onMounted } from 'vue';

// Az options paraméter elhagyásával, csak a refresh funkciót használjuk
const { data, refresh } = await useAsyncGql('getProductCategories');

// Computed property használata a biztonságos adateléréshez
const productCategories = computed(() => 
  data.value?.productCategories?.nodes || []
);

// Komponens aktiválásakor frissítjük az adatokat
onMounted(() => {
  // Explicit refresh a komponens betöltésekor
  refresh();
});
</script>

<template>
  <main class="container">
    <div v-if="productCategories.length"
      class="grid grid-cols-2 gap-4 my-6 md:grid-cols-3 lg:gap-8 xl:grid-cols-4">
      <CategoryCard 
        v-for="(category, i) in productCategories" 
        :key="category.id || i" 
        :node="category"
        :image-loading="i <= 2 ? 'eager' : 'lazy'" 
      />
    </div>
  </main>
</template>