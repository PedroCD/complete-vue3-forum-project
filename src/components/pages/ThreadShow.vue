<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <post-list :posts="threadPosts" />
    <post-editor @save="addPost"/>
  </div>
</template>

<script setup>
import sourceData from '@/data.json'
import PostList from '@/components/PostList.vue'
import { computed, ref, defineProps } from 'vue'
import PostEditor from '@/components/PostEditor.vue'

const threads = ref(sourceData.threads)
const posts = ref(sourceData.posts)
const newPostText = ref('')

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

const addPost = (eventData) => {
  const post = {
    ...eventData.post,
    threadId: props.id
  }
  posts.value.push(post)
  thread.value.posts.push(post.id)
  newPostText.value = ''
}
</script>

<style scoped>

</style>
