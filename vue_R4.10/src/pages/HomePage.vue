<script setup>
import { ref, computed } from "vue"
import PostCard from "@/components/PostCard.vue"

const texte = ref(" ")
const trimedText = computed(() => texte.value.trim())
const postlist = ref([])
const sortedPosts = computed(() => [...postlist.value].sort((a, b) => b.createdAt - a.createdAt))

function deletePost(id) {
  postlist.value = postlist.value.filter((post) => post.id !== id)
}

function likePost(id) {
  const post = postlist.value.find((post) => post.id === id)
  post.liked = !post.liked
}

function addPost() {
  const newPost = {
    id: Math.random.toString(36).substring(2),
    content: texte.value.trim(),
    createdAt: new Date(),
    author: {
      username: "la calotte de vos morts",
      avatarUrl:
        "https://i.ytimg.com/vi/EXeGmtBdH6M/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGGUgUChVMA8=&rs=AOn4CLBRQv4p8ER6wjwUj8TVVF_dH6yi-g",
    },
  }
  postlist.value.push(newPost)
  /*postlist.value.sort(function (a, b) {
    return a.createdAt < b.createdAt
  })*/
  texte.value = ""
  //console.log(postlist)
}
//let texte ="vinicius la merde";
/*function updateText(event){
  texte.value = event.target.value
}
  */

const apiPosts = ref([])
function fetchPosts() {
  const result = fetch("https://posts-crud-api.vercel.app/posts")
  result
    .then((response) => response.json())
    .then((data) => {
      apiPosts.value = data
    })
}

fetchPosts()
</script>

<template>
  <main>
    <div class="container">
      <form class="card" @submit.prevent="addPost">
        <textarea name="post" id="post" placeholder="Ecrit gitan" v-model="texte"></textarea>
        <button type="submit" :disabled="!trimedText">Publier</button>
      </form>

      <h2 v-show="apiPosts.length == 0">Aucun posts pour le moment</h2>

      <PostCard
        v-for="(post, index) in apiPosts"
        :key="index"
        :postlists="post"
        @delete="deletePost"
        @like="likePost"
      />

      <!--<article v-for="(postlists, index) in sortedPosts" :key="index" class="card">
        <header>
          <img :src="postlists.author.avatar" alt="avatar" width="166" height="166" />
          <a> {{ postlists.author.username }}</a>
        </header>
        <p>{{ postlists.content }}</p>
      </article>
      -->
    </div>
  </main>
</template>
