<template>
  <div>
    <v-toolbar flat>
      <v-btn text color="blue" style="margin-right: 10px;">
        <span style="color: blue; text-transform: none;">
          Export CSV
        </span>
      </v-btn>
      <v-btn color="blue" @click="showNuevo = true">
        <span style="color: white; text-transform: none;">
          Add Students
        </span>
      </v-btn>
      <v-spacer />
      <v-icon left>
        mdi-bell
      </v-icon>
      <v-btn text color="blue" style="text-align: right; margin-right: 50px;">
        <span style="color: black; text-transform: none;">
          Log out
        </span>
      </v-btn>
    </v-toolbar>

    <v-container>
      <v-row class="mt-3">
        <v-col cols="1">
          <v-select
            v-model="filter"
            :items="filterOptions"
            label="Filter"
            outlined
            dense
          />
        </v-col>
        <v-col cols="6">
          <v-text-field
            v-model="search"
            prepend-inner-icon="mdi-magnify"
            label="Search for a student by name or email"
            outlined
            hide-details
          />
        </v-col>
      </v-row>
      <v-row class="mt-3">
        <v-col cols="12">
          <v-data-table
            :headers="headers"
            :items="filteredStudents"
            elevation="0"
            style="width: 100% !important;"
          />
        </v-col>
      </v-row>
    </v-container>
    <v-dialog v-model="showNuevo" max-width="1100" persistent @click:outside="closeDialog">
      <v-card
        style="overflow: hidden; width: 100%; height: 90vh; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 50px;"
      >
        <v-card-title class="text-h4" style="text-align: left; width: 100%;">
          &nbsp;&nbsp;Add Students
        </v-card-title>
        <v-card-title class="text-h5" style="text-align: left; width: 100%; margin-bottom: 20px;">
          &nbsp;&nbsp;&nbsp;Manually&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Import CSV
        </v-card-title>
        &nbsp;
        &nbsp;
        <v-card-text style="width: 100%; display: flex; justify-content: left;">
          <v-form ref="form" v-model="validForm" style="width: 80%;">
            <v-container>
              <v-row>
                <v-col cols="4">
                  Name
                  <v-text-field
                    v-model="studentName"
                    :rules="[v => !!v || 'Field is required']"
                    outlined
                    type="text"
                    style="margin-bottom: 20px;"
                  />
                </v-col>
                <v-col cols="4">
              &nbsp;
                  <v-select
                    v-model="classNameStu"
                    :rules="[v => !!v || 'Field is required']"
                    outlined
                    placeholder="Class"
                    :items="['JSS 1', 'JSS 2', 'JSS 3', 'SS 1','SS 2','SS 3']"
                    style="margin-bottom: 20px; margin-left: 20px;"
                  />
                </v-col>
                <v-col cols="4">
              &nbsp;
                  <v-select
                    v-model="genderNameStu"
                    :rules="[v => !!v || 'Field is required']"
                    outlined
                    placeholder="Gender"
                    :items="['Male', 'Female', 'Other']"
                    style="margin-bottom: 20px; margin-left: 20px;"
                  />
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="6">
                  Email address
                  <v-text-field
                    v-model="schoolEmailStu"
                    :rules="emailValidation"
                    outlined
                    type="email"
                    style="margin-bottom: 20px;"
                  />
                </v-col>
                <v-col cols="6">
                  Phone number
                  <v-text-field
                    v-model="phoneNumberStu"
                    :rules="[v => !!v || 'Field is required']"
                    outlined
                    type="text"
                    style="margin-bottom: 20px;"
                  />
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="6">
                  Password
                  <v-text-field
                    v-model="passwordStu"
                    :rules="passwordValidation"
                    outlined
                    type="password"
                    style="margin-bottom: 20px;"
                  />
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </v-card-text>

        <v-card-actions style="width: 100%; display: flex; justify-content: center; margin-left: 40px;">
          <v-row style="width: 80%;">
            <v-col cols="2">
              <v-btn
                plain
                block
                color="white"
                style="border: none; display: flex; align-items: center; justify-content: center;"
                @click="addAnother"
              >
                <span style="color: black; text-transform: none;">
                  + Add Another
                </span>
              </v-btn>
            </v-col>
            <v-col cols="2">
              <v-btn flat block color="#d3d3d3" style="border: none; display: flex; align-items: center; justify-content: center;" @click="agregar">
                <span style="color: black; text-transform: none;">
                  Add student
                </span>
              </v-btn>
            </v-col>
          </v-row>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  data () {
    return {
      headers: [
        { text: 'Name', align: 'left', sortable: true, value: 'nameStu' },
        { text: 'Student ID', align: 'left', sortable: true, value: 'id' },
        { text: 'Email Address', align: 'left', sortable: true, value: 'emailStu' },
        { text: 'Class', align: 'left', sortable: true, value: 'classStu' },
        { text: 'Gender', align: 'left', sortable: true, value: 'genderStu' }
      ],
      token: null,
      estudiantes: [],
      showNuevo: false,
      validForm: false,
      search: '',
      studentName: null,
      schoolEmailStu: null,
      phoneNumberStu: null,
      passwordStu: null,
      classNameStu: null,
      genderNameStu: null,
      ageNumStu: null,
      passwordValidation: [
        v => (v && v.length > 8) || 'Password must be more than 8 characters'
      ],
      emailValidation: [
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ]
    }
  },
  computed: {
    filteredStudents () {
      return this.estudiantes.filter((student) => {
        const searchTerm = this.search.toLowerCase()
        return (
          student.nameStu.toLowerCase().includes(searchTerm) ||
          student.emailStu.toLowerCase().includes(searchTerm)
        )
      })
    }
  },
  mounted () {
    this.token = localStorage.getItem('token')
    console.log(this.token)
    if (!this.token) {
      this.$router.push('/')
    }
    this.getAllStudents()
  },
  methods: {
    getAllStudents () {
      const url = '/api/auth/get-all-student'
      const config = {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      }
      console.log(config)
      this.$axios.get(url, config)
        .then((res) => {
          console.log('@@ res => ', res)
          if (res.data.message === 'Success') {
            this.estudiantes = res.data.students
          } else if (res.data.message === 'Invalid Token') {
            this.$router.push('/')
          }
        })
        .catch((err) => {
          this.$router.push('/')
          console.log('@@@ err => ', err)
        })
    },
    closeDialog () {
      this.showNuevo = false
    },
    agregar () {
      this.validForm = this.$refs.form.validate()
      if (this.validForm) {
        const sendData = {
          id: Date.now().toString(),
          nameStu: this.studentName,
          emailStu: this.schoolEmailStu,
          classStu: this.classNameStu,
          genderStu: this.genderNameStu,
          phoneStu: this.phoneNumberStu,
          passwordStu: this.passwordStu,
          ageStu: this.ageNumStu
        }
        console.log('@@@ data => ', sendData)
        const config = {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
        const url = '/api/auth/registrar-estudiante'
        this.$axios.post(url, sendData, config)
          .then((res) => {
            console.log('@@@ res => ', res)
            if (res.data.message === 'Estudiante Registrado Satisfactoriamente') {
              this.getAllStudents()
              this.showNuevo = false
            }
          })
          .catch((err) => {
            console.log('@@@ err => ', err)
          })
      } else {
        alert('Faltan Datos')
      }
    },
    addAnother () {
      this.validForm = this.$refs.form.validate()
      if (this.validForm) {
        const sendData = {
          id: Date.now().toString(),
          nameStu: this.studentName,
          emailStu: this.schoolEmailStu,
          classStu: this.classNameStu,
          genderStu: this.genderNameStu,
          phoneStu: this.phoneNumberStu,
          passwordStu: this.passwordStu,
          ageStu: this.ageNumStu
        }
        console.log('@@@ data => ', sendData)
        const config = {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
        const url = '/api/auth/registrar-estudiante'
        this.$axios.post(url, sendData, config)
          .then((res) => {
            console.log('@@@ res => ', res)
            if (res.data.message === 'Estudiante Registrado Satisfactoriamente') {
              this.getAllStudents()
              // Limpiar los campos del formulario
              this.studentName = ''
              this.classNameStu = ''
              this.genderNameStu = ''
              this.schoolEmailStu = ''
              this.phoneNumberStu = ''
              this.passwordStu = ''
              this.ageNumStu = ''
            }
          })
          .catch((err) => {
            console.log('@@@ err => ', err)
          })
      } else {
        alert('Faltan Datos')
      }
    }
  }
}
</script>
