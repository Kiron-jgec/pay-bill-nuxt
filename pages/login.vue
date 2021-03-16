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
          style="flex-direction-column;"
          class="dataContainer mt-3"
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
          style="flex-direction-column;"
          class="dataContainer mt-3"
        >
        <h1 class="">Log In</h1>
          <v-form ref="form" v-model="valid" lazy-validation>
           

            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="E-mail"
              required
               prepend-inner-icon="mdi-email-outline"
              class="mt-2"
            ></v-text-field>

            <v-text-field
              v-model="password"
              :rules="passwordRules"
              label="Type pasword"
              required
              class="mt-2"
              type="password"
              prepend-inner-icon="mdi-lock-outline"
            ></v-text-field>
           


          

           

            

            <v-btn color="#1365ff" class="white--text" >
              Log In
            </v-btn>
            <span> Forget password ? <a href=""> Click Here</a> </span>




          </v-form>



          <div class="socialLogin text-center mt-6">
             <v-divider></v-divider>
              <h4 class="my-2">Log In With</h4>
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
}
img {
  width: 100%;
}
.container {
  width: 100vw !important;
  padding: 5% !important;
}
</style>
