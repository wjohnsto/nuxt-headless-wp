<template>
  <div class="container">
    <div>
      <h1 class="text-center">Nuxt Headless WordPress Demo</h1>
      <div class="container py-4 posts">
        <div class="row">
          <post-card v-for="post in posts" :key="post.slug" :post="post" />
          <div class="d-flex w-100">
            <div class="ml-auto" v-if="pageInfo.hasNextPage">
              <NuxtLink :to="{ query: { after: pageInfo.endCursor } }"
                ><span>Next Page</span></NuxtLink
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { PostsState } from '~/store/posts'

const pageCount = 5

export default Vue.extend({
  computed: {
    posts() {
      return (this.$store.state.posts as PostsState).nodes
    },
    pageInfo() {
      return (this.$store.state.posts as PostsState).pageInfo
    },
  },
  watch: {
    async $route() {
      await this.$nuxt.refresh()
      window.scrollTo(0, 0)
    },
  },
  async asyncData({ store, query }) {
    await store.dispatch('posts/getPosts', {
      after: query.after,
      before: query.before,
      first: query.before ? undefined : pageCount,
      last: query.before ? pageCount : undefined,
    })
  },
})
</script>

<style>
</style>
