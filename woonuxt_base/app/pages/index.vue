<script setup>
import CategoriesContent from '~/pages/categories.vue';
</script>

<template>
  <main>
    <Hero />
    <NextHero />
    
    <!-- Direkt beillesztjük a kategóriák oldalról származó komponenst -->
    <div class="container py-12">
      <h2 class="text-2xl font-bold mb-6">Termékkategóriák</h2>
      <!-- A CategoriesContent komponens fog gondoskodni a kategóriák lekérdezéséről és megjelenítéséről -->
      <CategoriesContent />
    </div>
    
    <AboutSec />
    <BlogSec />
  </main>
</template>

<style scoped>
.brand img {
  max-height: min(8vw, 120px);
  object-fit: contain;
  object-position: center;
}
</style>