<template>
  <select :value="$props.filterValue" @change="$emit('update:filterValue', ($event.target as HTMLSelectElement).value)">
    <option disabled value="">Select category</option>
    <option v-for="category in categories" :value="category">
      {{ category.charAt(0).toUpperCase() + category.slice(1) }}
    </option>
  </select>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const categories = ref<string[]>([])

defineProps({
  filterValue: {
    type: String,
    required: true
  }
})

const emits = defineEmits(['update:filterValue'])

const fetchCategories = async () => {
  try {
    const res = await fetch('https://fakestoreapi.com/products/categories')

    if (res.ok){
      const data = await res.json()
      categories.value = data
    }
  } catch (err){
    console.error(err)
  }
}

fetchCategories()
</script>

<style scoped lang="scss">

</style>