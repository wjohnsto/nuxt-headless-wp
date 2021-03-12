<template>
  <article class="col-12 py-5">
    <div class="card shadow">
      <div class="card-body">
        <h5 class="card-title">
          <NuxtLink :to="{ name: 'slug', params: { slug: post.slug } }">{{
            post.title
          }}</NuxtLink>
        </h5>
        <!-- eslint-disable-next-line vue/no-v-html -->
        <div class="card-text" v-html="post.excerpt"></div>
      </div>
    </div>
  </article>
</template>

<script lang="ts">
import { PropsDefinition } from 'vue/types/options'
import { Post } from '~/store/posts'

export default {
  props: ['post'] as PropsDefinition<{ post: Post }>,
}
</script>
