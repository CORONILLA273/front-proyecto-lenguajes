<template>
  <v-col cols="12">
    <v-row>
      <v-btn block color="blue" @click="showNuevo = true">
        <span style="color: white; text-transform: none;">
          Add Teachers
        </span>
      </v-btn>
    </v-row>
    <v-row class="mt-3">
      <v-data-table
        :headers="headers"
        :items="maestros"
        elevation="0"
        style="width: 100% !important;"
      />
    </v-row>
    <v-dialog v-model="showNuevo" width="400" persistent>
      <v-card-title>Add Teachers</v-card-title>
      <v-card-text>
        <v-form ref="form" v-model="validForm">
          <v-text-field
            v-model="teacherName"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Full Name"
            type="text"
          />
          <v-text-field
            v-model="emailTeacher"
            :rules="emailValidation"
            class="fixed-width"
            outlined
            placeholder="Enter the Email Address"
            type="email"
          />
          <v-text-field
            v-model="phoneNumberTeacher"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Phone number"
            type="text"
          />
          <v-text-field
            v-model="passwordTeacher"
            :rules="passwordValidation"
            class="fixed-width"
            outlined
            placeholder="Enter the password"
            type="password"
          />
          <v-text-field
            v-model="classNameTeacher"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Class"
            type="text"
          />
          <v-text-field
            v-model="subjectTeacher"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the subject"
            type="text"
          />
          <v-text-field
            v-model="genderNameTeacher"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the Gender"
            type="text"
          />
          <v-text-field
            v-model="designationTeacher"
            :rules="[v => !!v || 'Field is required']"
            class="fixed-width"
            outlined
            placeholder="Enter the designation"
            type="text"
          />
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-row>
          <v-col cols="6">
            <v-btn block color="primary" @click="agregar">
              <span style="color: white; text-transform: none;">
                Add Teacher
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
          value: 'nameTea' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Subject', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'subjectTea' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Class', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'classTea' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Email Address', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'emailTea' // Esto es para el nombred el elemento que viene en la base de datos.
        },
        {
          text: 'Gender', // Esto es para el texto del encabezado
          align: 'left', // Esto es para alinearlo
          sortable: true, // esto es ordenar descedente y ascedente
          value: 'genderTea' // Esto es para el nombred el elemento que viene en la base de datos.
        }
      ],
      token: null,
      maestros: [],
      showNuevo: false,
      validForm: false,
      // Space
      teacherName: null,
      emailTeacher: null,
      phoneNumberTeacher: null,
      passwordTeacher: null,
      classNameTeacher: null,
      subjectTeacher: null,
      genderNameTeacher: null,
      designationTeacher: null,

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
    this.getAllTeachers()
  },
  methods: {
    getAllTeachers () {
      const url = '/api/auth/get-all-teachers'
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
            this.maestros = res.data.teachers
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
          nameTea: this.teacherName,
          emailTea: this.emailTeacher,
          phoneTea: this.phoneNumberTeacher,
          passwordTea: this.passwordTeacher,
          classTea: this.classNameTeacher,
          subjectTea: this.subjectTeacher,
          genderTea: this.genderNameTeacher,
          designationTea: this.designationTeacher
        }
        console.log('@@@ data => ', sendData)
        const config = {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
        const url = '/api/auth/registrar-profesor'
        this.$axios.post(url, sendData, config)
          .then((res) => {
            console.log('@@@ res => ', res)
            if (res.data.message === 'Profesor Registrado Satisfactoriamente') {
              this.getAllTeachers()
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
