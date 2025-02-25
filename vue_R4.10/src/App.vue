<script setup>
import { ref, computed } from "vue"

const texte = ref(" ")
const trimedText = computed(() => texte.value.trim())
const postlist = ref([])
function addPost() {
  const newPost = {
    id: Math.random.toString(36).substring(2),
    content: texte.value.trim(),
    createdAt: new Date(),
    author: {
      username: "no",
      avatar:
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSmT7PcffnQYc1ulaxJKGBQvfV2Uq7mXwqcRw&s",
    },
  }
  postlist.value.push(newPost)
  postlist.value.sort(function (a, b) {
    return a.createdAt < b.createdAt
  })
  texte.value = ""
  //console.log(postlist)
}
//let texte ="vinicius la merde";
/*function updateText(event){
  texte.value = event.target.value
}
  */
</script>
<template>
  <main>
    <div class="container">
      <form class="card" @submit.prevent="addPost">
        <textarea name="post" id="post" placeholder="Ecrit gitan" v-model="texte"></textarea>
        <button type="submit" :disabled="!trimedText">Publier</button>
      </form>

      <h2 v-show="postlist.length == 0">Aucun posts pour le moment</h2>

      <article v-for="(postlists, index) in postlist" :key="index" class="card">
        <header>
          <img :src="postlists.author.avatar" alt="avatar" width="166" height="166" />
          <a> {{ postlists.author.username }}</a>
        </header>
        <p>{{ postlists.content }}</p>
      </article>
    </div>
  </main>
</template>
<style scoped>
.container {
  height: 100vh;
  margin: 0 auto;
  max-width: 640px;
}
.card {
  background-color: var(--color-bg-secondary);
  border-radius: 10px;
  border: 1px solid var(--color-border);
  margin-bottom: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  margin-top: 1rem;
  padding: 1rem 1.5rem;
  width: 100%;
}
textarea {
  background: none;
  border: none;
  color: var(--color-text-primary);
  flex: 1;
  margin-bottom: 1rem;
  outline: none;
  padding: 0.5rem 0;
  resize: none;
  field-sizing: content;
}
button {
  align-self: flex-end;
  background: none;
  border-radius: 10px;
  border: 1px solid var(--color-border);
  color: var(--color-text-primary);
  cursor: pointer;
  font-size: 1rem;
  height: 40px;
  padding: 0 1rem;
}

button:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

article {
  padding: 1rem;
  overflow: hidden;
}

article p {
  white-space: pre-wrap;
}

article header {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}
</style>
