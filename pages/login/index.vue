<template>
  <v-app>
    <v-main>
      <div style="background-color: #f1f1f1;">
        <v-container
          class="d-flex flex-column align-center justify-center"
          style="min-height: 100vh;"
        >
          <v-card flat style="width: 600px; height: 700px; margin-top: 15px;" align="center" class="d-flex flex-column align-center justify-center">
            <v-card-title class="justify-center" style="font-size: 30px; margin-bottom: 30px">
              Welcome, Log into you account
            </v-card-title>
            <v-card-text align="center">
              <b>It is our great pleasure to have <br> you on board!</b>
            </v-card-text>
            <v-card-text align="center">
              <v-form>
                <!-- Modificar por "nombre escuela"-->
                <v-text-field
                  v-model="email"
                  class="fixed-width"
                  outlined
                  placeholder="Enter the email"
                  type="text"
                />
                <v-text-field
                  v-model="password"
                  :type="showPassword ? 'text' : 'password'"
                  label="Password"
                  outlined
                  class="fixed-width"
                  :append-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                  @click:append="togglePasswordVisibility"
                />
              </v-form>
            </v-card-text>
            <v-card-actions class="justify-center">
              <v-btn
                block
                color="blue"
                elevation="0"
                class="fixed-width"
                style="height: 50px; width: 700px;"
                @click="login"
              >
                <span style="text-transform: none; color: white;">
                  Login
                </span>
              </v-btn>
            </v-card-actions>
            <div style="display: flex; align-items: center;">
              <v-card-text style="margin-right: 0px;">
                Already have an account?
              </v-card-text>
              <router-link to="/signup" style="text-decoration: none; color: blue;">
                Signup
              </router-link>
            </div>
          </v-card>
        </v-container>
      </div>
    </v-main>
  </v-app>
</template>

<script>
export default {
  layout: 'no-sideBar',
  data () {
    return {
      email: '',
      password: '',

      showPassword: true
    }
  },
  methods: {
    async login () {
      try {
        const response = await this.$axios.post('/api/auth/login', {
          email: this.email,
          password: this.password
        })
        if (response.data.token) {
          console.log('Login successful', response.data.token)
        }
      } catch (error) {
        if (error.response) {
          console.error('Error response:', error.response.data)
        } else {
          console.error('Error', error.message)
        }
      }
    },
    signupUser () {
      // Lógica de registro de usuario
    },
    finish () {
      // Lógica al finalizar el stepper
    },
    togglePasswordVisibility () {
      this.showPassword = !this.showPassword
    }
  }
}
</script>

<style scoped>
.fixed-width {
  max-width: 300px;
  width: 100%;
}

.stepper-card {
  max-width: 1200px; /* Agranda el tamaño del v-card */
  width: 150%;
  margin-top: 16px; /* Espacio entre los dos v-card */
}

.v-stepper__step--active .v-stepper__step__title {
  font-weight: bold;
}

.v-stepper__step__title {
  text-align: center;
  display: block;
  width: 100%;
  margin-top: 8px; /* Ajusta este valor según sea necesario */
}

.equal-height {
  height: 700px; /* Ajusta la altura del v-card principal */
}
</style>
