<script setup>
import { ref } from "vue";

const texte = ref("vinicius la merde");
const postlist = ref([]);
function addPost(){
  postlist.value.push(texte.value);
  texte.value = "";
  console.log(postlist);
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
        <textarea name="post" id="post" placeholder="Ecrit fdp" v-model="texte" ></textarea>
        <button type="submit">Publier</button>
      </form>

      <p v-for="(postlists, index) in postlist" :key="index">{{ postlists }}</p>
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
</style>