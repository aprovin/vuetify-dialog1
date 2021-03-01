<template>
<v-app>
    <v-app-bar color="primary" dark dense app clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>TITLE</v-toolbar-title>
      <div class="flex-grow-1"></div>

      <v-menu bottom transition="slide-y-transition">
        <template v-slot:activator="{ on }">
          <v-btn dark icon v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list dense>
          <v-list-item key="Help">
            <v-list-item-title>Help</v-list-item-title>
          </v-list-item>
          <v-list-item key="About">
            <v-list-item-title>About</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <v-navigation-drawer :value="showDrawer" class="drawer" clipped app>
      <v-list nav dense>

        <v-list-item key="key1">
          <v-list-item-icon>
            <v-icon>mdi-email-multiple</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Emails</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list-item key="key2">
          <v-list-item-icon>
            <v-icon>mdi-folder</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Folders</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

      </v-list>
    </v-navigation-drawer>


    <v-main>
      <v-container fluid fill-height>
        <transition name="fade" mode="out-in" appear>
          <compo></compo>
        </transition>
      </v-container>
    </v-main>

  </v-app>
</template>

<script>
import Compo from './components/Compo.vue'

export default {
  name: 'App',
  components: {
    Compo
  },
  data: () => ({
    drawer: true,
  }),
  computed: {
    showDrawer () {
      if(this.drawer)
        return true
      return false
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
