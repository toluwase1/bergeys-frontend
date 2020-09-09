<template>
  <v-app>
    <v-card width="400px" class="mx-auto mt-5">

      <!-- <Notification :message="error" v-if="error"/> -->

      <v-card-title>
        <h2 color="green"> Register </h2>
      </v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field
            v-model="email"
            name="email"
            :error-messages="emailErrors"
            label="Email" filled rounded
            required
            @input="$v.email.$touch()"
            @blur="$v.email.$touch()"
            prepend-icon="mdi-mail"
          />

          <v-text-field label="Username" filled rounded
            v-model="username"
            name="username"
            prepend-icon="mdi-account-circle"
          />
          <v-text-field
            v-model="password"
            name="password"
            :type="showPassword ? 'text' : 'password'"
            label="Password" filled rounded
            prepend-icon="mdi-lock"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
          />
          <v-divider></v-divider>

          <v-card-actions>

            <v-btn color="success" rounded @click="register">
              Register
            </v-btn>
            <v-spacer></v-spacer>
            <v-card-actions>
      
    </v-card-actions>
          </v-card-actions>

        </v-form>
        
      </v-card-text>

      <v-divider> </v-divider>
      
         <v-card-actions>
        <!-- <v-btn color="success">Register </v-btn> -->
        
        <nuxt-link to="/register">
          <v-btn color="success" rounded>
            Register
          </v-btn>
        </nuxt-link>
        
        <v-spacer> </v-spacer>
        <nuxt-link to="/">
         <v-btn color="info" rounded>
            Login
         </v-btn>
        </nuxt-link>
      </v-card-actions>
    </v-card>
    
  </v-app>
</template>

<script>
  // import Notification from '~/components/Notification'
  import {validationMixin} from "vuelidate";
  import {required, minLength, email, sameAs} from "vuelidate/lib/validators";
  export default {
    middleware: 'guest',
    // components: {
    //   Notification,
    // },
    mixins: [validationMixin],
    validations: {
      name: {required, minLength: minLength(4)},
      email: {required, email},
      password: {required, minLength: minLength(6)},
      confirmPassword: {sameAsPassword: sameAs("password")}
    },
    data() {
      return {
        username: '',
        email: '',
        password: '',
        error: null
      }
    },
    methods: {
      async register() {
        try {
          await this.$axios.post('register', {
            username: this.username,
            email: this.email,
            password: this.password
          })
          await this.$auth.loginWith('local', {
            data: {
              email: this.email,
              password: this.password
            },
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
    font-family: 'Quicksand',
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