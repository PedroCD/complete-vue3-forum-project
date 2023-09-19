<template>
  <ForumList
      v-for="category in categories"
      :key="category.id"
      :forums="getForumsForCategory(category)"
      :title="category.name"
      :category-id="category.id"
  />
</template>

<script setup>
import { defineProps } from 'vue'
import ForumList from '@/components/ForumList.vue'
import sourceData from '@/data.json'

// eslint-disable-next-line no-unused-vars
const props = defineProps({
  categories: {
    required: true,
    type: Array
  }
})

const getForumsForCategory = (category) => {
  return sourceData.forums.filter(forum => forum.categoryId === category.id)
}

</script>

<style >

</style>
