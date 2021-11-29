<template>
  <v-app @changeMsg="setMessage">
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-icon>
        mdi-camera-burst
      </v-icon>
      <v-toolbar-title class="ml-1" v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item>
          <v-list-item-action>
            <v-icon light> mdi-account-circle </v-icon>
          </v-list-item-action>
          <v-list-item-title>{{ this.user.email }}</v-list-item-title>
        </v-list-item>
        <v-list-item class="pointer" @click="onLogout">
          <v-list-item-action>
            <v-icon light> mdi-logout </v-icon>
          </v-list-item-action>
          <v-list-item-title>Sair</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>{{title}} &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'GridPics',
      user: {
        email: window.localStorage.getItem('email'),
      },
    }
  },
  methods: {
    onLogout() {
      this.$router.push({ path: '/' })
    },
  },
}
</script>
