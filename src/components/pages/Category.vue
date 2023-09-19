<template>
  <h1>{{category.name}}</h1>
  <ForumList
      :title="category.name"
      :forums="getForumsForCategory(category)"
  />
</template>
<script setup>
import { computed, defineProps } from 'vue'
import sourceData from '@/data.json'
import ForumList from '@/components/ForumList.vue'

// eslint-disable-next-line no-unused-vars
const props = defineProps({
  id: {
    required: true,
    type: String
  }
})

const category = computed(() => {
  return sourceData.categories.find(category => category.id === props.id)
})

const getForumsForCategory = (category) => {
  return sourceData.forums.filter(forum => forum.categoryId === category.id)
}

</script>

<style scoped>

</style>
