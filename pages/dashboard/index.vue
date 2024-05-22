<template>
  <v-app>
    <v-main>
      <v-container
        class="d-flex flex-column align-center justify-center"
        style="min-height: 100vh;"
      >
        <!-- Main Card -->
        <v-card flat style="width: 600px; height: 700px; margin-top: 15px;" align="center" class="d-flex flex-column align-center justify-center">
          <v-stepper v-model="step">
            <v-stepper-items>
              <!-- Step 1 -->
              <v-stepper-content step="1">
                <v-card flat>
                  <v-card-title style="font-size: 30px; margin-bottom: 30px;">
                    Welcome, create your school account
                  </v-card-title>
                  <v-card-text
                    class="black--text text-center align-center"
                    style="font-size: 18px; margin-bottom: 20px; line-height: 32px;"
                  >
                    It is our great pleasure to have <br> you on board!
                  </v-card-text>
                  <v-card-text align="center">
                    <v-form>
                      <v-text-field
                        v-model="adminName"
                        class="fixed-width"
                        outlined
                        placeholder="Enter the name of admin"
                        type="text"
                      />
                      <v-text-field
                        v-model="schoolName"
                        class="fixed-width"
                        outlined
                        placeholder="Enter the name of school"
                        type="text"
                      />
                      <v-text-field
                        v-model="schoolEmail"
                        class="fixed-width"
                        outlined
                        placeholder="Enter the school email"
                        type="email"
                      />
                    </v-form>
                  </v-card-text>
                  <v-card-actions class="justify-center">
                    <v-btn
                      color="blue"
                      elevation="0"
                      class="fixed-width"
                      style="height: 50px;"
                      @click="step = 2"
                    >
                      <span style="text-transform: none; color: white;">
                        Next
                      </span>
                    </v-btn>
                  </v-card-actions>
                  <v-card-actions class="justify-center">
                    <div style="display: flex; align-items: center;">
                      <v-card-text style="margin-right: 0px;">
                        Already have an account?
                      </v-card-text>
                      <router-link to="/signup" style="text-decoration: none; color: blue;">
                        Signup
                      </router-link>
                    </div>
                  </v-card-actions>
                </v-card>
              </v-stepper-content>

              <!-- Step 2 -->
              <v-stepper-content step="2">
                <v-card style="width: 550px; height: 600px; margin-top: 30px;">
                  <v-card-title class="text-center" style="font-size: 29px; margin-bottom: 30px; margin-top: 100px">
                    Udemy school, Choose your password
                  </v-card-title>
                  <v-card-text align="center">
                    <v-form>
                      Choose a password
                      <v-text-field
                        v-model="password"
                        :type="showPassword ? 'text' : 'password'"
                        label="Password"
                        outlined
                        class="fixed-width"
                        :append-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                        @click:append="togglePasswordVisibility"
                      />
                      Confirm password
                      <v-text-field
                        v-model="confirmPassword"
                        :type="showPassword ? 'text' : 'password'"
                        label="Password"
                        outlined
                        class="fixed-width"
                        :append-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                        @click:append="togglePasswordVisibility"
                      />
                      Must be at least 8 characters
                    </v-form>
                  </v-card-text>
                  <v-card-actions class="justify-center">
                    <v-btn
                      color="blue"
                      elevation="0"
                      class="fixed-width"
                      style="height: 50px;"
                      @click="step = 3"
                    >
                      <span style="text-transform: none; color: white;">
                        Next
                      </span>
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-stepper-content>

              <!-- Step 3 -->
              <v-stepper-content step="3">
                <v-card flat style="width: 550px; height: 600px; margin-top: 30px;">
                  <v-card-title style="font-size: 29px; margin-bottom: 30px; margin-top: 100px">
                    Udemy school, Choose your password
                  </v-card-title>
                  <v-card-text align="center">
                    <v-form>
                      <v-text-field
                        v-model="staffNumber"
                        class="fixed-width"
                        outlined
                        placeholder="Number of staff"
                        type="password"
                      />
                      <v-select
                        v-model="schoolAddress"
                        :items="schoolAddresses"
                        label="Select a school address"
                        outlined
                        class="fixed-width"
                      />
                      Must be at least 8 characters
                    </v-form>
                  </v-card-text>
                  <v-card-actions class="justify-center">
                    <v-btn
                      color="blue"
                      elevation="0"
                      class="fixed-width"
                      style="height: 50px;"
                      @click="step = 4"
                    >
                      <span style="text-transform: none; color: white;">
                        Next
                      </span>
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-stepper-content>

              <!-- Step 4 -->
              <v-stepper-content step="4">
                <v-card flat style="width: 550px; height: 600px; margin-top: 30px;">
                  <v-card-title class="justify-center" style="font-size: 30px; margin-bottom: 30px">
                    Welcome, Log into you account
                  </v-card-title>
                  <v-card-text align="center">
                    <b>It is our great pleasure to have <br> you on board!</b>
                  </v-card-text>
                  <v-card-text align="center">
                    alo
                  </v-card-text>
                  <v-card-actions class="justify-center">
                    <v-btn
                      color="blue"
                      elevation="0"
                      class="fixed-width"
                      style="height: 50px;"
                      @click="signupUser()"
                    >
                      <span style="text-transform: none; color: white;">
                        login
                      </span>
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-stepper-content>
            </v-stepper-items>
          </v-stepper>
        </v-card>
        <!-- Stepper Card -->
        <v-card flat elevation="0" class="stepper-card">
          <v-stepper v-model="step" alt-labels>
            <v-stepper-header>
              <v-stepper-step :complete="step > 1" step="1">
                Your details <br> Name and email
              </v-stepper-step>
              <v-divider />
              <v-stepper-step :complete="step > 2" step="2">
                Choose a password <br> Choose a secure password
              </v-stepper-step>
              <v-divider />
              <v-stepper-step :complete="step > 3" step="3">
                Invite your team <br> Start collaborating
              </v-stepper-step>
              <v-divider />
              <v-stepper-step :complete="step > 4" step="4">
                Additional Information <br> Provide more details
              </v-stepper-step>
            </v-stepper-header>
          </v-stepper>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      adminName: null,
      schoolName: null,
      schoolEmail: null,
      password: null,
      confirmPassword: null,
      staffNumber: null,
      schoolAddress: null,
      step: 1,

      showPassword: true,

      selectedAddress: '',
      schoolAddresses: [
        '1234 Elm Street, Springfield, IL 62701, USA',
        '5678 Maple Avenue, Lakeside, CA 92040, USA',
        '9101 Oak Drive, Boulder, CO 80301, USA',
        '1122 River Road, Riverside, OH 45431, USA',
        '3344 Sunset Boulevard, Miami, FL 33133, USA',
        '5566 Willow Lane, Austin, TX 78701, USA',
        '7788 Hilltop Street, San Francisco, CA 94110, USA',
        '9900 Cedar Avenue, Cedar Grove, NJ 07009, USA',
        '12345 Pine Ridge Road, Atlanta, GA 30301, USA',
        '67890 Oakwood Lane, Oakwood, OH 44146, USA'
      ]
    }
  },
  methods: {
    signupUser () {
      const sendData = {
        adminName: this.adminName,
        schoolName: this.schoolName,
        schoolEmail: this.schoolEmail,
        password: this.password,
        staffNumber: this.staffNumber,
        schoolAddress: this.schoolAddress,
        id: Date.now().toLocaleString()
      }
      console.log('@@@ data => ', sendData)
      const url = '/api/auth/signup'
      this.$axios.post(url, sendData)
        .then((res) => {
          if (res.data.message === 'Usuario Registrado Satisfactoriamnete') {
            console.log('Se logro registrar')
          }
        })
        .catch((err) => {
          console.log('@@@ err => ', err)
        })
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
