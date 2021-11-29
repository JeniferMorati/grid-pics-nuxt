<template>
  <div class="home">
    <Post
      v-for="post in newPosts"
      v-bind:key="post.id"
      :title="post.title"
      :img="post.img"
      :description="post.description"
    />
  </div>
</template>

<script>
import posts from '../mocks/posts'

export default {
  data() {
    return {
      newPosts: posts,
    }
  },
  layout: 'logged',
}
</script>

<style scoped>
.home {
  max-width: 1200px;
  margin: 0 auto;
  column-count: 4;
}

@media (max-width: 1200px) {
  .home {
    column-count: 3;
  }
}

@media (max-width: 700px) {
  .home {
    column-count: 2;
  }
}

@media (max-width: 460px) {
  .home {
    column-count: 1;
  }
}
</style>
