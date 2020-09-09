<template>
<v-app>

  <v-card
    color="grey lighten-4"
    flat
    height="200px"
    tile
  >
    <v-toolbar dense>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>Bergeys Manual</v-toolbar-title>

      <v-spacer></v-spacer>

    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn flat>
        <nuxt-link to="/">
            Home
        </nuxt-link>
        </v-btn>

        <v-btn flat>
        <nuxt-link to="/about">
            About
        </nuxt-link>
        </v-btn>

        <v-btn flat>
        <nuxt-link to="/contact">
           Contact
        </nuxt-link>
        </v-btn>

      </v-toolbar-items>

      <div class="navbar-menu">
        <div class="navbar-end">
          <div class="navbar-item has-dropdown is-hoverable" v-if="isAuthenticated">
            <!--a class="navbar-link">
              {{ loggedInUser.username }}
            </a-->
            <nuxt-link class="navbar-item" to="/profile">{{ loggedInUser.username }}</nuxt-link>
            <a class="navbar-item" @click="logout">Logout</a>
          </div>
          <template v-else>
            <nuxt-link class="navbar-item" to="/register">Register</nuxt-link>
            <nuxt-link class="navbar-item" to="/">Log In</nuxt-link>
          </template>
        </div>
      </div>

      

      <!--v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn-->
    </v-toolbar>
  <nuxt/>
  </v-card>

  </v-app>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  
  methods: {
    async logout() {
      await this.$auth.logout();
    },
  },

  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  }
}
</script>

<style>
html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>
