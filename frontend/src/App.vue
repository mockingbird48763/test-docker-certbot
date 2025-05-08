<script setup>
import {http} from '@/api/http.js'
import {ref, onMounted} from 'vue'
const data = ref({
  userId: 0,
  id: 0,
  title: 'no title',
  body: 'no body'
})
const postId = ref(1)
const imageUrl = "/images/example/20000000_000000_0001.jpg"

const fetchPost = async (id) => {
  const res = await http.get(`/posts/${id}`)
  data.value = res.data
}

onMounted(async() => {
  await fetchPost(postId.value)
})
</script>

<template>
  <nav><h1>Posts</h1></nav>
  <main>
  <input v-model="postId" type="number" />
  <button @click="fetchPost(postId)">Fetch Post</button>
  </main>
  <body>
    <div>userId: {{ data.userId }}</div>
    <div>id: {{ data.id }}</div>
    <div>title: {{ data.title }}</div>
    <div>body: {{ data.body }}</div>
    <div>
      <img :src="imageUrl" />
    </div>
  </body>
</template>