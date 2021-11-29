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
          <img class="post-image" :src="img" alt="Foto do post" />
          <span class="subtitle-1 pa-3">{{ title }}</span>
        </v-card>
      </v-hover>
    </template>
    <template v-slot:default="dialog">
      <v-card class="modal">
        <v-img :lazy-src="img" :src="img" alt="Foto do post"></v-img>
        <v-card-text>
          <p class="subtitle-1 mt-1">{{ title }}</p>
        </v-card-text>
        <v-card-text>
          <div>{{ description }}</div>
        </v-card-text>
        <v-btn
          color="white"
          class="modal-close"
          @click="dialog.value = false"
          elevation="2"
          icon
        >
          <v-icon light> mdi-close </v-icon>
        </v-btn>
      </v-card>
    </template>
  </v-dialog>
</template>

<script>
export default {
  props: {
    title: { type: String, required: true },
    img: { type: String, required: true },
    description: { type: String, required: true },
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
  border: 1px solid transparent;
}

.on-hover {
  border: 1px solid white;
}

.modal {
  position: relative;
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
</style>
>
