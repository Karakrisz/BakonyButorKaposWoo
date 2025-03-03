<script lang="ts" setup>
// Az adatlekérést az index komponensben végezzük
import { computed, onMounted } from 'vue';

const { data, refresh } = await useAsyncGql('getProductCategories');
const productCategories = computed(() => 
  data.value?.productCategories?.nodes || []
);

// Minden alkalommal frissítsünk, amikor a főoldalra navigálunk
onMounted(() => {
  refresh();
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