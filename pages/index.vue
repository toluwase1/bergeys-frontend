<template>
  <v-app>
    <v-card width="400px" class="mx-auto mt-5">
      <v-card-title>
      <h1> Bergey's Login </h1>
      </v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field label = "Username"
          prepend-icon="mdi-account-circle"
           />
           <v-text-field
           :type ="showPassword ? 'text' : 'password'"
           label ="Password"
           prepend-icon="mdi-lock"
           :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
           @click:append= "showPassword = !showPassword"
          />
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
export default {
data: ()=> ({
  showPassword: false
})

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
