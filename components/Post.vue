<template>
  <v-dialog max-width="600">
    <template v-slot:activator="{ on, attrs }">
      <v-hover v-slot="{ hover }">
        <v-card
          v-bind="attrs"
          v-on="on"
          :class="{ 'on-hover': hover }"
          class="post d-flex align-start flex-column justify-center"
        >
          <div class="featured"></div>
          <img class="post-image" :src="img" alt="Foto do post" />
          <div class="post-title">
            <span class="title-overflow">{{ title }}</span>
            <div>
              <v-icon>mdi-comment-text</v-icon>
              {{ comments.length }}
            </div>
          </div>
        </v-card>
      </v-hover>
    </template>
    <template v-slot:default="dialog">
      <v-card class="modal">
        <v-img
          :lazy-src="img"
          :src="img"
          max-width="500px"
          max-height="550px"
          min-height="550px"
          alt="Foto do post"
        ></v-img>
        <div class="featured"></div>
        <v-card-text class="title-container">
          <span class="subtitle-1">{{ title }}</span>
          <p>{{ description }}</p>
        </v-card-text>
        <v-btn @click="openComments" class="mx-2 comment-button" fab dark small>
          <v-icon dark> mdi-comment-plus </v-icon>
        </v-btn>

        <div class="chvron-up-container" :class="{ 'comments-open': isOpen }">
          <div class="posts-container">
            <v-card-text>
              <div class="my-2">
                <v-icon class="mr-1" dark> mdi-account-circle </v-icon>
                <span>{{ user }}</span>
              </div>
              <v-textarea
                outlined
                v-model="userComment"
                name="coment"
                :counter="280"
                label="Comente sobre isso!"
                value=""
                rows="1"
              ></v-textarea>
              <v-btn
                @click="onSubmitComment(id)"
                color="primary"
                elevation="2"
                small
              >
                Comentar
              </v-btn>
            </v-card-text>
            <v-card-text class="comments-container">
              <div
                v-for="comment in comments"
                v-bind:key="comment.id"
                class="comment-container py-3 my-2"
              >
                <div class="pa-3" v-if="comment.comment">
                  <p>
                    <v-icon dark> mdi-account-circle </v-icon>
                    {{ comment.author }}
                  </p>
                  <div>
                    <p>{{ comment.comment }}</p>
                  </div>
                </div>
              </div>
            </v-card-text>
          </div>
          <v-btn
            @click="openComments"
            class="mx-2 comment-button"
            fab
            dark
            small
          >
            <v-icon dark> mdi-comment-remove </v-icon>
          </v-btn>
        </div>

        <v-btn
          color="white"
          class="modal-close"
          @click="
            () => {
              dialog.value = false;
              isOpen = false;
            }
          "
          elevation="2"
          icon
        >
          <v-icon dark> mdi-close </v-icon>
        </v-btn>
      </v-card>
    </template>
  </v-dialog>
</template>

<script>
const getUser = () => window.localStorage.getItem('email');

export default {
  data() {
    return {
      userComment: '',
      user: getUser(),
      isOpen: false,
    }
  },
  props: {
    title: { type: String, required: true },
    img: { type: String, required: true },
    description: { type: String, required: true },
    comments: { type: Array, require: true },
    id: { type: Number, required: true },
  },
  methods: {
    onSubmitComment(id) {
      this.$emit('comment-submit', {
        id,
        comment: {
          author: this.user,
          comment: this.userComment,
        },
      })
      this.userComment = '';
    },
    openComments() {
      this.isOpen = !this.isOpen;
    },
  },
}
</script>

<style lang="css" scoped>
.post {
  cursor: pointer;
  transition: border 0.3s ease;
  break-inside: avoid-column;
  overflow: hidden;
  transform: scale(0.95);
  border: 1px solid white;
}

.on-hover {
  border: 1px solid #1976d2;
}

.modal {
  position: relative;
}

.featured {
  height: 100%;
  position: absolute;
  bottom: 0;
  width: 100%;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.9) 20%, transparent 40%);
}

.modal-close {
  position: absolute;
  top: 5px;
  right: 5px;
}

.post-image {
  display: block;
  width: 100%;
}

.comment-container {
  border: 1px solid gray;
  border-radius: 5px;
}

.comments-container {
  max-height: 350px;
  overflow: auto;
}
.post-title {
  position: absolute;
  z-index: 1;
  bottom: 0px;
  left: 0px;
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.title-overflow {
  width: 150px;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}

.chvron-up-container {
  position: absolute;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  bottom: 0;
  height: 0%;
  overflow: hidden;
  width: 100%;
  transition: 0.3s;
}

.comments-open {
  height: 100%;
}

.comment-button {
  position: absolute;
  bottom: 10px;
  right: 5px;
}

.posts-container {
  height: 100%;
  background-color: rgba(18, 18, 18, 0.9);
  backdrop-filter: blur(2px);
  width: 100%;
}

.title-container {
  position: absolute;
  bottom: 0;
}
</style>
