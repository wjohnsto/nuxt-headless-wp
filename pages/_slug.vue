<template>
  <div class="container">
    <h1 class="text-center">{{ post.title }}</h1>
    <article class="py-5" v-html="post.content"></article>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  computed: {
    post() {
      return this.$store.state.posts.post
    },
  },
  async asyncData({ store, params }) {
    await store.dispatch('posts/getPost', params.slug)
  },
})
</script>
