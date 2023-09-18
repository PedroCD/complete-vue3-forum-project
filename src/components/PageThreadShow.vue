<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <div class="post-list">
      <div class="post"
           v-for="postId in thread.posts"
           :key="postId"
      >

        <div class="user-info">
          <a href="#" class="user-name">{{userById(postById(postId).userId).name}}</a>

          <a href="#">
            <img :src="userById(postById(postId).userId).avatar" alt="" class="avatar-large">
          </a>

          <p class="desktop-only text-small">107 posts</p>
        </div>

        <div class="post-content">
          <div>
            <p>
              {{posts.find(p => p.id === postId).text}}
            </p>
          </div>
        </div>

        <div class="post-date text-faded">
          {{postById(postId).publishedAt}}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import sourceData from '@/data.json'
import { computed, ref, defineProps } from 'vue'
// import { useRoute } from 'vue-router'

// const route = useRoute()

const threads = ref(sourceData.threads)
const posts = ref(sourceData.posts)
const users = ref(sourceData.users)

const props = defineProps({
  id: {
    required: true,
    type: String
  }
})

const thread = computed(() => {
  return threads.value.find(thread => thread.id === props.id)
})

function postById (postId) {
  return posts.value.find(p => p.id === postId)
}

function userById (userId) {
  return users.value.find(u => u.id === userId)
}
</script>

<style scoped>

</style>
