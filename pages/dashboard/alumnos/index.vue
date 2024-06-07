<template>
  <v-app>
    <v-container>
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

      <v-row class="mt-3">
        <v-col cols="1" style="margin-left: 20px;">
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
      <v-row>
        <v-col cols="8">
          <v-data-table
            :headers="headers"
            :items="filteredStudents"
            elevation="0"
            style="width: 100% !important;"
            hide-default-header
            hide-default-footer
            item-value="id"
            class="custom-table"
            disable-pagination
            :items-per-page="-1"
          >
            <template #item="{ item, index }">
              <tr
                :class="{'row-hover': hoveredRow === index, 'row-selected': selectedRow === item.id}"
                @mouseover="hoveredRow = index"
                @mouseleave="hoveredRow = null"
                @click="selectRow(item)"
              >
                <td class="custom-cell">
                  <div class="custom-cell-content">
                    <img :src="getAvatarUrl(item.id)" alt="avatar" class="avatar">
                    <span>{{ item.nameStu }}</span>
                  </div>
                </td>
                <td class="custom-cell">
                  {{ item.id }}
                </td>
                <td class="custom-cell">
                  {{ item.emailStu }}
                </td>
                <td class="custom-cell">
                  {{ item.classStu }}
                </td>
                <td class="custom-cell">
                  {{ item.genderStu }}
                </td>
              </tr>
            </template>
            <template #header="{ props }">
              <tr class="custom-header">
                <th v-for="header in props.headers" :key="header.text" class="custom-header-cell">
                  {{ header.text }}
                </th>
              </tr>
            </template>
          </v-data-table>
        </v-col>

        <v-col cols="4">
          <v-card v-if="selectedStudent" class="mx-auto" max-width="313" flat>
            <v-card-title class="text-center">
              <div class="text-center" style="width: 95%; font-size: 16px; color: #424242; font-weight: 500;">
                {{ selectedStudent.id }}
              </div>
            </v-card-title>
            <v-card-text class="text-center">
              <div style="text-align: center;">
                <img :src="getAvatarUrl(selectedStudent.id)" alt="avatar" class="avatar" style="width: 180px; height: 180px; font-size: 16px;">
                <div style="font-weight: 700; font-size: 16px; color:#1A1A1A; padding-top: 15px; padding-bottom: 6px;">
                  {{ selectedStudent.nameStu }}
                </div>
                <div>{{ selectedStudent.classStu }}</div>
                <div class="icons" style="padding-top: 14px; padding-bottom: 30px;">
                  <img :src="teacherIcon" alt="Teacher" class="icon">
                  <img :src="callCallingIcon" alt="Call Calling" class="icon">
                  <img :src="smsIcon" alt="SMS" class="icon">
                </div>
                <div class="about-section" style="color: black; font-size: 12px; padding-bottom: 100px;">
                  About
                </div>
                <div class="info-section">
                  <div class="info-item">
                    <div class="info-label">
                      Age
                    </div>
                    <div style="font-size: 14px; font-weight: 500;">
                      {{ selectedStudent.ageStu }}
                    </div>
                  </div>
                  <div class="info-item">
                    <div class="info-label">
                      Gender
                    </div>
                    <div>{{ selectedStudent.genderStu }}</div>
                  </div>
                </div>
                <div class="about-section" style="color: black; font-size: 12px;">
                  People from the same class
                </div>
              </div>
            </v-card-text>
          </v-card>
        </v-col>

        <v-dialog v-model="showNuevo" max-width="1100" persistent @click:outside="closeDialog">
          <v-card style="overflow: hidden; width: 100%; height: 90vh; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 50px;">
            <v-card-title class="text-h4" style="text-align: left; width: 100%;">
              &nbsp;&nbsp;Add Students
            </v-card-title>
            <v-card-title class="text-h5" style="text-align: left; width: 100%; margin-bottom: 20px;">
              &nbsp;&nbsp;&nbsp;Manually&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Import CSV
            </v-card-title>
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
                      <v-select
                        v-model="classNameStu"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        placeholder="Class"
                        :items="['JSS 1', 'JSS 2', 'JSS 3', 'SS 1', 'SS 2', 'SS 3']"
                        style="margin-bottom: 20px; margin-left: 20px;"
                      />
                    </v-col>
                    <v-col cols="4">
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
                      Add Student
                    </span>
                  </v-btn>
                </v-col>
              </v-row>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import callCallingIcon from '../../../assets/svg/call-calling.png'
import smsIcon from '../../../assets/svg/sms.png'
import teacherIcon from '../../../assets/svg/teacher.png'

export default {
  data () {
    return {
      headers: [
        {
          text: 'Name',
          align: 'left',
          sortable: true,
          value: 'nameStu'
        },
        {
          text: 'Student ID',
          align: 'left',
          sortable: true,
          value: 'id'
        },
        {
          text: 'Email Address',
          align: 'left',
          sortable: true,
          value: 'emailStu'
        },
        {
          text: 'Class',
          align: 'left',
          sortable: true,
          value: 'classStu'
        },
        {
          text: 'Gender',
          align: 'left',
          sortable: true,
          value: 'genderStu'
        }
      ],
      token: null,
      estudiantes: [],
      search: '', // Agregar esta línea
      filterOptions: ['Option1', 'Option2'], // Agregar opciones de filtro
      showNuevo: false,
      validForm: false,
      studentName: null,
      schoolEmailStu: null,
      phoneNumberStu: null,
      passwordStu: null,
      classNameStu: null,
      genderNameStu: null,
      ageNumStu: null,
      hoveredRow: null,
      selectedRow: null,
      selectedStudent: null, // Estudiante seleccionado

      // Íconos
      callCallingIcon,
      smsIcon,
      teacherIcon,

      passwordValidation: [
        v => (v && v.length > 8) || 'Password must have be more than 8 chars'
      ],
      emailValidation: [
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ]
    }
  },
  computed: {
    filteredStudents () {
      const searchTerm = this.search.toLowerCase()
      return this.estudiantes.filter((student) => {
        return (
          student.nameStu.toLowerCase().includes(searchTerm) ||
          student.emailStu.toLowerCase().includes(searchTerm)
        )
      })
    }
  },
  mounted () {
    this.token = localStorage.getItem('token')
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
      this.$axios.get(url, config)
        .then((res) => {
          if (res.data.message === 'Success') {
            this.estudiantes = res.data.students
          } else if (res.data.message === 'Invalid Token') {
            this.$router.push('/')
          }
        })
        .catch((err) => {
          this.$router.push('/')
          console.log(err)
        })
    },
    getAvatarUrl (id) {
      const hash = this.hashCode(id)
      const avatarId = hash % 70
      return `https://i.pravatar.cc/208?img=${avatarId + 1}`
    },
    hashCode (str) {
      let hash = 0
      for (let i = 0; i < str.length; i++) {
        const char = str.charCodeAt(i)
        hash = (hash * 32) - hash + char
        hash |= 0
      }
      return Math.abs(hash)
    },
    closeDialog () {
      this.showNuevo = false
    },
    selectRow (student) {
      this.selectedRow = student.id
      this.selectedStudent = student
      this.hoveredRow = null
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
        const config = {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
        const url = '/api/auth/registrar-estudiante'
        this.$axios.post(url, sendData, config)
          .then((res) => {
            if (res.data.message === 'Estudiante Registrado Satisfactoriamente') {
              this.getAllStudents()
              this.showNuevo = false
            }
          })
          .catch((err) => {
            console.log(err)
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

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

.custom-table {
  font-weight: 500;
  padding: 16px;
  font-family: 'Kumbh Sans', sans-serif;
  color: #4F4F4F;
}

.custom-header {
  background-color: #f5f5f5; /* Puedes ajustar el color de fondo si lo deseas */
}

.custom-header-cell {
  font-weight: 700;
  padding: 16px;
  text-align: left;
  font-size: 14px; /* Ajusta el tamaño de la letra aquí */
  color: #4F4F4F;
}

.custom-cell {
  color: #4F4F4F;
}

.custom-cell-content {
  display: flex;
  align-items: center;
}

.avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  margin-right: 8px;
}

.cell-text {
  color: inherit; /* Inherit color from parent */
}

.row-hover {
  background-color: #D5E7F6 !important; /* Azul claro para el hover */
}

.row-selected {
  background-color: #509CDB !important; /* Azul claro para la selección */
  color: white !important; /* Color del texto blanco */
}

.row-selected .custom-cell,
.row-selected .custom-cell .cell-text {
  color: white !important; /* Asegura que el texto de las celdas sea blanco */
}

.v-data-table tbody tr {
  cursor: pointer;
  color: #4F4F4F;
  height: 55px; /* Aumentar la altura de cada fila */
  line-height: 55px; /* Ajustar la altura de línea para centrar el contenido verticalmente */
}

.icons {
  margin-top: 16px;
}

.icon {
  width: 44px;
  height: 44px;
  margin: 0 8px;
  padding: 10px;
}

.about-section {
  font-weight: bold;
  font-size: 16px;
  text-align: left;
  margin: 16px 0;
}
.info-section {
  display: flex;
  justify-content: space-between;
  margin: 16px 0;
  text-align: left;
}
.info-item {
  width: 50%;
}
.info-label {
  font-weight: 600;
  font-size: 12px;
  padding-bottom: 3px;
  color: #1A1A1A;
}
</style>
