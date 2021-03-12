<template>
  <article class="col-12 py-5">
    <div class="card shadow">
      <div class="card-body">
        <h5 class="card-title">
          <NuxtLink :to="{ name: 'slug', params: { slug: post.slug } }">{{
            post.title
          }}</NuxtLink>
        </h5>
        <div class="card-text" v-html="post.excerpt"></div>
      </div>
    </div>
  </article>
</template>

<script lang="ts">
export default {
  props: ['post'],
}
</script>
