<script setup>
import { TrashIcon, HandThumbUpIcon } from "@heroicons/vue/24/outline"
import { HandThumbUpIcon as SolidHandThumbUpIcon } from "@heroicons/vue/24/solid"
import { useRouter } from "vue-router"

const props = defineProps({
  postlists: {
    type: Object,
    required: true,
  },
})

const router = useRouter()

const emit = defineEmits(["delete", "like"])

function deletePost() {
  emit("delete", props.postlists.id)
}

function likePost() {
  emit("like", props.postlists.id)
}

function goToUserProfile() {
  router.push({ name: "user", params: { username: props.postlists.author.username } })
}
</script>

<template>
  <article class="card">
    <header>
      <img :src="postlists.author.avatarUrl" alt="avatar" width="50" height="50" class="avatar" />
      <a @click="goToUserProfile"> {{ postlists.author.username }}</a>
    </header>
    <p>{{ postlists.content }}</p>

    <footer>
      <button @click="deletePost" class="btn-icon">
        <TrashIcon />
      </button>
      <button @click="likePost" class="btn-icon">
        <HandThumbUpIcon v-if="!postlists.liked" />
        <SolidHandThumbUpIcon v-else class="active" />

        <!-- <component
          :is="postlists.liked ? SolidHandThumbUpIcon : HandThumbUpIcon"
          :class="{ active: postlists.liked }"
        />  -->
      </button>
    </footer>
  </article>
</template>
