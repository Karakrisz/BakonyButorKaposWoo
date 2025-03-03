<script lang="ts" setup>
// Az adatlekérést az index komponensben végezzük
import { onMounted } from 'vue';

const { data, refresh } = await useAsyncGql('getProductCategories');

// A TypeScript típushibák elkerülése érdekében computed property-t használunk
// Ez hasonlít az eredeti kódodhoz, de frissíti az adatot az onMounted-ben
const productCategories = computed(() => data.value?.productCategories?.nodes || []);

// Frissítés betöltéskor és időközönként
onMounted(() => {
  // Azonnali frissítés
  refresh();
  
  // Periodikus frissítés csak produkcióban
  if (process.client && window.location.hostname !== 'localhost') {
    const timer = setInterval(() => {
      refresh();
    }, 30000);
    
    // Leállítás, amikor a komponens megsemmisül
    onBeforeUnmount(() => {
      clearInterval(timer);
    });
  }
});

// Navigáció figyelése
const route = useRoute();
watch(() => route.path, (newPath, oldPath) => {
  if (newPath === '/' && oldPath !== '/') {
    refresh();
  }
});
</script>

<template>
  <main>
    <Hero />
    <NextHero />
    <!-- <Discounts /> -->
    <CategorySec :categories="productCategories" />
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