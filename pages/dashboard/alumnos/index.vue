<template>
  <v-col cols="12">
    <v-row>
      <v-btn block color="blue" @click="showNuevo = true">
        <span style="color: white; text-transform: none;">
          Add Students
        </span>
      </v-btn>
    </v-row>
    <v-row class="mt-3">
      <v-data-table
        :headers="headers"
        :items="estudiantes"
        elevation="0"
        style="width: 100% !important;"
      />
    </v-row>
    <v-dialog v-model="showNuevo" width="400" persistent>
      <v-card-title>Add Students</v-card-title>
      <v-card-text>
        <v-form ref="form" v-model="validForm">
          <v-text-field
            v-model="studentName"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the name of student"
            type="text"
          />
          <v-text-field
            v-model="schoolEmailStu"
            :rules="emailValidation"
            class="fixed-width"
            outlined
            placeholder="Enter the school email"
            type="email"
          />
          <v-text-field
            v-model="phoneNumberStu"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Phone number"
            type="text"
          />
          <v-text-field
            v-model="passwordStu"
            :rules="passwordValidation"
            class="fixed-width"
            outlined
            placeholder="Enter the password"
            type="password"
          />
          <v-text-field
            v-model="classNameStu"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Class"
            type="text"
          />
          <v-text-field
            v-model="genderNameStu"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Gender"
            type="text"
          />
          <v-text-field
            v-model="ageNumStu"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the age"
            type="text"
          />
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-row>
          <v-col cols="6">
            <v-btn block color="primary" @click="agregar">
              <span style="color: white; text-transform: none;">
                Add student
              </span>
            </v-btn>
          </v-col>
          <v-col cols="6">
            <v-btn block color="green" @click="borrar">
              <span style="color: white; text-transform: none;">
                Add Another
              </span>
            </v-btn>
          </v-col>
        </v-row>
      </v-card-actions>
    </v-dialog>
  </v-col>
</template>

<script>
export default {
  data () {
    return {
      headers: [
        {
          text: 'Name', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'nameStu' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Student ID', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'id' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Email Address', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'emailStu' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Class', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'classStu' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Gender', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'genderStu' // Esto es para el nombred el elemento que viene en la base de datos.
        }
      ],
      token: null,
      estudiantes: [],
      showNuevo: false,
      validForm: false,
      // Space
      studentName: null,
      schoolEmailStu: null,
      phoneNumberStu: null,
      passwordStu: null,
      classNameStu: null,
      genderNameStu: null,
      ageNumStu: null,

      passwordValidation: [
        v => (v && v.length > 8) || 'Password must have be more than 8 chars'
      ],
      emailValidation: [
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ]
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
    }
  }
}
</script>
