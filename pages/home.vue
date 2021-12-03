<template>
  <div class="home">
    <Post
      v-on:comment-submit="onFetchComments"
      v-for="post in newPosts"
      v-bind:key="post.id"
      :id="post.id"
      :title="post.title"
      :img="post.img"
      :description="post.description"
      :comments="post.comments"
    />
  </div>
</template>

<script>
import dbPosts from '../mocks/posts';

const newPosts = dbPosts.posts.map((post) => ({
  id: post.id,
  title: post.title,
  img: post.img,
  description: post.description,
  comments: post.comments || [],
}));

const user = window.localStorage.getItem('email');

export default {
  data() {
    return {
      newPosts,
      user,
    }
  },
  layout: 'logged',
  methods: {
    onFetchComments(e) {
      const data = newPosts.filter((items) => items.id === e.id)[0];
      data.comments.push(e.comment);
    },
  },
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
