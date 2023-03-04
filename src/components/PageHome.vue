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
  <div v-for="thread in threads" :key="thread.id" class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <div class="post-list">
      <div class="post" v-for="postId in thread.posts" :key="postId">
        <div class="user-info">
          <a href="#" class="user-name">{{ getUserById(getPostById(postId).userId).name }}</a>

          <a href="#">
            <img
              class="avatar-large"
              :src="getUserById(getPostById(postId).userId).avatar"
              alt=""
            />
          </a>

          <p class="desktop-only text-small">107 posts</p>
        </div>

        <div class="post-content">
          <div>
            <p>
              {{ getPostById(postId).text }}
            </p>
          </div>
        </div>

        <div class="post-date text-faded">
          {{ getPostById(postId).publishedAt }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
