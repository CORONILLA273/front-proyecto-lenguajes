<template>
  <v-app>
    <v-main>
      <v-container
        class="d-flex flex-column align-center justify-center"
        style="min-height: 100vh;"
      >
        <!-- Main Card -->
        <v-card flat style="width: 600px; height: 700px; margin-top: 15px;" align="center" class="d-flex flex-column align-center justify-center">
          <v-stepper v-model="step" flat>
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
                        :rules="[v => !!v || 'Field is required']"
                        class="fixed-width"
                        outlined
                        placeholder="Enter the name of admin"
                        type="text"
                      />
                      <v-text-field
                        v-model="schoolName"
                        :rules="[v => !!v || 'Field is required']"
                        class="fixed-width"
                        outlined
                        placeholder="Enter the name of school"
                        type="text"
                      />
                      <v-text-field
                        v-model="schoolEmail"
                        :rules="emailValidation"
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
                      class="fixed-width"
                      style="height: 50px;"
                      @click="nextStep(1)"
                    >
                      <span style="text-transform: none; color: white;">
                        Next
                      </span>
                    </v-btn>
                  </v-card-actions>
                  <v-card-actions class="justify-center">
                    <div style="display: flex; align-items: center; white-space: nowrap;">
                      <v-card-text style="margin-right: 0px;">
                        Already have an account?
                        <router-link to="/login" style="text-decoration: none; color: blue;">
                          Sign in
                        </router-link>
                      </v-card-text>
                    </div>
                  </v-card-actions>
                </v-card>
              </v-stepper-content>

              <!-- Step 2 -->
              <v-stepper-content step="2">
                <v-card flat style="width: 550px; height: 600px; margin-top: 30px;">
                  <v-card-title class="text-center" style="font-size: 29px; margin-bottom: 30px; margin-top: 100px">
                    Udemy school, Choose your password
                  </v-card-title>
                  <v-card-text align="center">
                    <v-form>
                      Choose a password
                      <v-text-field
                        v-model="password"
                        :rules="passwordValidation"
                        :type="showPassword ? 'password' : 'text'"
                        label="Password"
                        outlined
                        class="fixed-width"
                        :append-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                        @click:append="togglePasswordVisibility"
                      />
                      Confirm password
                      <v-text-field
                        v-model="confirmPassword"
                        :rules="passwordConfirmValidation"
                        :type="showPasswordConfirm ? 'password' : 'text'"
                        label="Password"
                        outlined
                        class="fixed-width"
                        :append-icon="showPasswordConfirm ? 'mdi-eye-off' : 'mdi-eye'"
                        @click:append="togglePasswordConfirmVisibility"
                      />
                      Must be at least 8 characters
                    </v-form>
                  </v-card-text>
                  <v-card-actions class="justify-center">
                    <v-btn
                      color="blue"
                      class="fixed-width"
                      style="height: 50px;"
                      @click="nextStep(2)"
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
                    Udemy school, Choose your staffs
                  </v-card-title>
                  <v-card-text align="center">
                    <v-form>
                      <v-text-field
                        v-model="staffNumber"
                        :rules="[v => !!v || 'Field is required', v => isPositiveInteger(v) || 'Must be a positive integer greater than zero']"
                        type="number"
                        class="fixed-width"
                        outlined
                        placeholder="Number of staff"
                      />
                      <v-select
                        v-model="schoolAddress"
                        :items="schoolAddresses"
                        :rules="[v => !!v || 'Field is required']"
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
                      class="fixed-width"
                      style="height: 50px;"
                      @click="nextStep(3)"
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
                    All right, let's start!
                  </v-card-title>
                  <v-card-text align="center">
                    <b>We're ready, are you too?</b>
                  </v-card-text>
                  <v-card-actions class="justify-center">
                    <v-btn
                      color="blue"
                      class="fixed-width"
                      style="height: 50px;"
                      @click="signupUser()"
                    >
                      <span style="text-transform: none; color: white;">
                        Finish
                      </span>
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-stepper-content>
            </v-stepper-items>
          </v-stepper>
        </v-card>
        <!-- Stepper Card -->
        <v-card flat class="stepper-card">
          <v-stepper v-model="step" flat alt-labels>
            <v-stepper-header>
              <v-stepper-step :complete="isStep1Complete" step="1">
                <div class="step-text">
                  Your details
                  <small>Name and email</small>
                </div>
              </v-stepper-step>
              <v-divider />
              <v-stepper-step :complete="isStep2Complete" step="2">
                <div class="step-text">
                  Choose a password
                  <small>Choose a secure password</small>
                </div>
              </v-stepper-step>
              <v-divider />
              <v-stepper-step :complete="isStep3Complete" step="3">
                <div class="step-text">
                  Invite your team
                  <small>Start collaborating</small>
                </div>
              </v-stepper-step>
              <v-divider />
              <v-stepper-step :complete="isStep4Complete" step="4">
                <div class="step-text">
                  Additional Information
                  <small>Provide more details</small>
                </div>
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
  layout: 'no-sideBar',
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
      showPasswordConfirm: true,

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
      ],

      passwordValidation: [
        v => (v && v.length > 8) || 'Password must have be more than 8 chars'
      ],
      passwordConfirmValidation: [
        v => (v && (v === this.password)) || 'Password fields must be same'
      ],
      emailValidation: [
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ]
    }
  },
  computed: {
    isStep1Complete () {
      return !!this.adminName && !!this.schoolName && !!this.schoolEmail
    },
    isStep2Complete () {
      return !!this.password && !!this.confirmPassword
    },
    isStep3Complete () {
      return !!this.staffNumber && !!this.schoolAddress
    },
    isStep4Complete () {
      return false
    }
  },
  methods: {
    isValidEmail (emailString) {
      const regex = /.+@.+\..+/
      return regex.test(emailString)
    },
    isPositiveInteger (value) {
      const number = Number(value)
      return Number.isInteger(number) && number > 0
    },
    nextStep (currentStep) {
      if (currentStep === 1 && this.isStep1Complete && this.isValidEmail(this.schoolEmail)) {
        this.step = 2
      } else if (currentStep === 2 && this.isStep2Complete && (this.password.length > 8) && (this.password === this.confirmPassword)) {
        this.step = 3
      } else if (currentStep === 3 && this.isStep3Complete && this.isPositiveInteger(this.staffNumber)) {
        this.step = 4
      }
    },
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
      this.$router.push('/login')
    },
    finish () {
      // Lógica al finalizar el stepper
    },
    togglePasswordVisibility () {
      this.showPassword = !this.showPassword
    },
    togglePasswordConfirmVisibility () {
      this.showPasswordConfirm = !this.showPasswordConfirm
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

.step-text {
  text-align: center;
}
</style>
