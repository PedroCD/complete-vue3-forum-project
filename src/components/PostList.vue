<template>
  <div class="post-list">
    <div class="post"
         v-for="post in posts"
         :key="post.id"
    >

      <div class="user-info">
        <a href="#" class="user-name" >{{userById(post.userId).name}}</a>

        <a href="#">
          <img :src="userById(post.userId).avatar" alt="" class="avatar-large">
        </a>

        <p class="desktop-only text-small">107 posts</p>
      </div>

      <div class="post-content">
        <div>
          <p>
            {{post.text}}
          </p>
        </div>
      </div>

      <div class='post-date text-faded'>
        <app-date :timestamp="post.publishedAt" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref } from 'vue'
import sourceData from '@/data.json'
import AppDate from '@/components/AppDate.vue'

// eslint-disable-next-line no-unused-vars
const props = defineProps({
  posts: {
    required: true,
    type: Array
  }
})

const users = ref(sourceData.users)

function userById (userId) {
  console.log(userId, users.value.find(u => u.id === userId))
  return users.value.find(u => u.id === userId)
}

</script>

<style>
</style>
