<template>
  <div class="col-full push-top">
    <div class="forum-header">
      <div class="forum-details">
        <h1>{{ forum.name }}</h1>
        <p class="text-lead">{{ forum.description }}</p>
      </div>
      <a href="new-thread.html" class="btn-green btn-small">Start a thread</a>
    </div>
  </div>

  <div class="col-full push-top">
    <ThreadList :threads="threads"/>
  </div>
</template>

<script setup>
import { computed, defineProps } from 'vue'
import ThreadList from '@/components/ThreadList.vue'
import sourceData from '@/data.json'

const props = defineProps({
  id: {
    required: true,
    type: String
  }
})

const forum = computed(() => {
  return sourceData.forums.find(forum => forum.id === props.id)
})

const threads = computed(() => {
  return sourceData.threads.filter(thread => thread.forumId === props.id)
})
</script>

<style>

</style>
