<template>
  <span :title="humanFriendlyDate(timestamp)">
    {{diffForHumans(timestamp)}}
  </span>
</template>

<script setup>
import { defineProps } from 'vue'
import dayjs from 'dayjs'
import relativeTime from 'dayjs/plugin/relativeTime'
import localizedDate from 'dayjs/plugin/localizedFormat'
dayjs.extend(relativeTime)
dayjs.extend(localizedDate)

const props = defineProps({
  timestamp: {
    required: true,
    type: Number
  }
})

const diffForHumans = () => {
  return dayjs.unix(props.timestamp).fromNow()
}

const humanFriendlyDate = () => {
  return dayjs.unix(props.timestamp).format('llll')
}
</script>

<style>

</style>
