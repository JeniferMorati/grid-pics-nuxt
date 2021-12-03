<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-icon> mdi-camera-burst </v-icon>
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
            <v-icon dark> mdi-account-circle </v-icon>
          </v-list-item-action>
          <v-list-item-title>{{ this.user.email }}</v-list-item-title>
        </v-list-item>
        <v-list-item class="pointer" @click="onLogout">
          <v-list-item-action>
            <v-icon dark> mdi-logout </v-icon>
          </v-list-item-action>
          <v-list-item-title>Sair</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>{{ title }} &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<style>
::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.1);
  background-color: transparent;
  border-radius: 10px;
}

::-webkit-scrollbar {
  width: 2px;
  background-color: rgba(0, 0, 0, 0.1);
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: #1976d2;
}
</style>

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
