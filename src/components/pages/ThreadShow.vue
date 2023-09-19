<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <post-list :posts="threadPosts" />

  </div>
</template>

<script setup>
import sourceData from '@/data.json'
import PostList from '@/components/PostList.vue'
import { computed, ref, defineProps } from 'vue'

const threads = ref(sourceData.threads)
const posts = ref(sourceData.posts)

const props = defineProps({
  id: {
    required: true,
    type: String
  }
})

const thread = computed(() => {
  return threads.value.find(thread => thread.id === props.id)
})

const threadPosts = computed(() => {
  return posts.value.filter(post => post.threadId === props.id)
})

</script>

<style scoped>

</style>
