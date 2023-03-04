<script setup>
import { ref } from 'vue'
import sourceData from '@/data.json'

const threads = ref(sourceData.threads)
const posts = ref(sourceData.posts)
const users = ref(sourceData.users)

function getPostById(postId) {
  return posts.value.find((post) => post.id === postId)
}

function getUserById(userId) {
  return users.value.find((user) => user.id === userId)
}
</script>

<template>
  <div v-for="thread in threads" :key="thread.id">
    <h2>{{ thread.title }}</h2>
    <div v-for="postId in thread.posts" :key="postId">
      <p>{{ getUserById(getPostById(postId).userId).name }}</p>
      <p>{{ getPostById(postId).text }}</p>
    </div>
  </div>
</template>

<style scoped></style>
