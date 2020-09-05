<template>
  <v-app>
    <v-card width="400px" class="mx-auto mt-5">
      <v-card-title>
        <h1> Register </h1>
      </v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field
            v-model="email"
            :error-messages="emailErrors"
            label="Email"
            required
            @input="$v.email.$touch()"
            @blur="$v.email.$touch()"
            prepend-icon="mdi-mail"
          />

          <v-text-field label="Username"
                        prepend-icon="mdi-account-circle"
          />
          <v-text-field
            :type="showPassword ? 'text' : 'password'"
            label="Password"
            prepend-icon="mdi-lock"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
          />

          <v-text-field
            v-model="password"
            :type="showPassword ? 'text' : 'password'"
            :error-messages="passwordErrors"
            label="Password"
            required
            @input="$v.password.$touch()"
            @blur="$v.password.$touch()"
            prepend-icon="mdi-lock"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
          />


        </v-form>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>


        <v-spacer></v-spacer>
        <v-btn color="success" @click.stop.prevent="register">
          Submit
        </v-btn>
      </v-card-actions>
    </v-card>
    <v-card-actions>
      <nuxt-link to="/register">
        <v-btn color="success">
          Register
        </v-btn>
      </nuxt-link>

      <v-spacer></v-spacer>
      <nuxt-link to="/">
        <v-btn color="info">
          Login
        </v-btn>
      </nuxt-link>
    </v-card-actions>
  </v-app>
</template>

<script>
  import {validationMixin} from "vuelidate";
  import {required, minLength, email, sameAs} from "vuelidate/lib/validators";

  export default {
    mixins: [validationMixin],
    validations: {
      name: {required, minLength: minLength(4)},
      email: {required, email},
      password: {required, minLength: minLength(6)},
      confirmPassword: {sameAsPassword: sameAs("password")}
    },
    data() {
      return {
        name: "",
        email: "",
        password: "",
        confirmPassword: "",
        status: null,
        showPassword: false
      }
    },
    methods: {
      register() {
        //this is a sample. you can write your code as you see fit
        alert("This will use axios to connect with the api. You should remove this alert afterwards")
        this.$axios.$post('/register', {
          email: this.email,
          name: this.name,
          password: this.password,
          //this will post the email, name and password to the api server
        })
          .then(response => {
            //do something when the response is a success
          })
          .catch(error => {
          })
//do something when there is a failure
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
