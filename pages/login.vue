<template>
  <v-app class="green">
    <v-card width="400px" class="mx-auto mt-5">

      <!-- <Notification :message="error" v-if="error"/> -->

      <v-card-title>
      <h2> Bergey's Login </h2>
      </v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field label="Email" filled rounded required
            v-model="email"
            name="email"
            prepend-icon="mdi-mail"
          />
          <v-text-field
            :type ="showPassword ? 'text' : 'password'"
            v-model="password"
            name="password"
            label="password" filled rounded
            prepend-icon="mdi-lock"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
           @click:append= "showPassword = !showPassword"
          />
          <v-divider></v-divider>
          
          <v-card-actions>

            <v-btn color="success" @click="login">
                Login
            </v-btn>
            <v-spacer></v-spacer>
          </v-card-actions>

        </v-form>
      </v-card-text>
      <v-divider> </v-divider>
      <v-card-actions>
        <!-- <v-btn color="success">Register </v-btn> -->
        
        <nuxt-link to="/register">
          <v-btn color="success">
            Register
          </v-btn>
        </nuxt-link>
        
        <v-spacer> </v-spacer>
        <nuxt-link to="/">
         <v-btn color="info">
            Login
         </v-btn>
        </nuxt-link>
      </v-card-actions>
    </v-card>

  </v-app>
</template>

<script>

import Notification from '~/components/Notification'

export default {
  middleware: 'guest',
  // components: {
  //   Notification,
  // },

  data() {
    return {
      email: '',
      password: '',
      error: null
    }
  },

  methods: {
    async login() {
      try {
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/home')
      } catch (e) {
        this.error = e.response.data.message
      }
    }
  }

};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
