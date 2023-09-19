<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <post-list :posts="threadPosts" />
    <div class="col-full">
      <form @submit.prevent="addPost">
        <div class="form-group">
          <textarea v-model="newPostText" name="" id="" cols="30" rows="10" class="form-input" />
        </div>
        <div class="form-actions">
          <button class="btn-blue">Submit post</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import sourceData from '@/data.json'
import PostList from '@/components/PostList.vue'
import { computed, ref, defineProps } from 'vue'

const threads = ref(sourceData.threads)
const posts = ref(sourceData.posts)
let newPostText = ref('')

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

const addPost = () => {
  const postId = 'ggg' + Math.random()
  const post = {
    id: postId,
    test: newPostText.value,
    publishedAt: Math.floor(Date.now() / 1000),
    threadId: props.id,
    userId: 'rpbB8C6ifrYmNDufMERWfQUoa202'
  }
  posts.value.push(post)
  thread.value.posts.push(post)
  newPostText = ''
}
</script>

<style scoped>

</style>
