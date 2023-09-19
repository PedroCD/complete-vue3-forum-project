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

      <div class="post-date text-faded" :title="humanFriendlyDate(post.publishedAt)">
        {{diffForHumans(post.publishedAt)}}
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref } from 'vue'
import sourceData from '@/data.json'
import dayjs from 'dayjs'
import relativeTime from 'dayjs/plugin/relativeTime'
import localizedDate from 'dayjs/plugin/localizedFormat'
dayjs.extend(relativeTime)
dayjs.extend(localizedDate)

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

const diffForHumans = (timestamp) => {
  return dayjs.unix(timestamp).fromNow()
}

const humanFriendlyDate = (timestamp) => {
  return dayjs.unix(timestamp).format('llll')
}

</script>

<style lang="scss" scoped>
</style>
