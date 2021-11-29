<template>
  <v-app @changeMsg="setMessage">
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-icon> mdi-camera-burst </v-icon>
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>{{ title }} &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      fixed: false,
      title: 'GridPics',
    }
  },
}
</script>
