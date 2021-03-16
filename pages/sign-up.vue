<template>
  <div class="signup">
    <v-container fluid class="containe">
      <v-layout row wrap justify-center justify-space-between>
        <v-flex
          xs12
          sm8
          md8
          lg8
          xl8
          column
          justify-center
          align-self-center
          style="flex-direction-column;"
          class="dataContainer"
        >
          <img
            src="../assets/images/login-pay-bill.svg"
            alt="signup-pay-bill"
          />
        </v-flex>

        <v-flex
          xs12
          sm4
          md4
          lg4
          xl4
          column
          justify-center
          align-self-center
          style="flex-direction-column;"
          class="dataContainer pa-4 "
          elevation-3
        >
        <h1 class="">Sign Up</h1>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="name"
              :counter="10"
              :rules="nameRules"
              label="Shop / Company Name"
              prepend-inner-icon=" mdi-store-outline "
              required
              class="mt-3"
            ></v-text-field>

            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="E-mail"
              required
               prepend-inner-icon="mdi-email-outline"
              class="mt-3"
            ></v-text-field>

            <v-text-field
              v-model="password"
              :rules="passwordRules"
              label="Type pasword"
              required
              class="mt-3"
              type="password"
              prepend-inner-icon="mdi-lock-outline"
            ></v-text-field>
               <v-text-field
              v-model="password"
              :rules="passwordRules"
              label="Repete Password"
              required
              class="mt-3"
              type="password"
              prepend-inner-icon=" mdi-lock-check-outline"
            ></v-text-field>


            <v-checkbox
              v-model="checkbox"
              :rules="[(v) => !!v || 'You must agree to continue!']"
              label="Do you agree?"
              required
              class="mt-2"
            ></v-checkbox>

           

            

            <v-btn color="#1365ff" class="white--text" >
              Sign Up
            </v-btn>




          </v-form>



          <div class="socialLogin text-center mt-6">
             <v-divider></v-divider>
              <h4 class="my-2">Sign up With</h4>
              <v-btn color="#1365ff" outlined >
              <v-icon>mdi-google</v-icon>
            </v-btn>
            <v-btn color="#1365ff" outlined >
                            <v-icon>mdi-facebook</v-icon>

            </v-btn>
          </div>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>
<script>
export default {
  layout: 'signUplogin', 
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      (v) => !!v || 'Name is required',
      (v) => (v && v.length <= 10) || 'Name must be less than 10 characters',
    ],
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    password:'',
    passwordRules: [
      (v) => !!v || 'Name is required',
      (v) => (v && v.length >= 6) || 'Name must be gretter than 6 characters',
    ],

    checkbox: false,
  }),

  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    },
  },
}
</script>
<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
h1 
{
    color: #1365ff;
}
.signup {
  width: 100vw !important;
 top: 0;
 height: 100vh;
}
img {
  width: 100%;
}
.container {
  width: 100vw !important;
  padding: 5% !important;
}
</style>
