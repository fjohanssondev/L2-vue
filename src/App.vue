<script setup lang="ts">
import { ref } from 'vue';
import ProductList from './components/product/ProductList.vue';
import Filter from './components/filter/Filter.vue';

const categoryRef = ref('')
</script>

<template>
  <h1>Welcome to your store!</h1>
  <header class="header">
    <h2>Products</h2>
    <Filter
      :filter-value="categoryRef"
      @update:filter-value="categoryRef = $event"
    />
  </header>
  <ProductList :filter-value="categoryRef" />
</template>

<style scoped lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
