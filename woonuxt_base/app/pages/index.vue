<script lang="ts" setup>
const { data } = await useAsyncGql('getProductCategories');
const productCategories = data.value.productCategories?.nodes as ProductCategory[];

</script>

<template>
  <main>
    <Hero />
    <NextHero />
    <!-- <Discounts /> -->
    <!-- <CategorySec /> -->
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