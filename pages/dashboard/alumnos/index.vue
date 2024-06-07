<template>
  <v-row>
    <v-col cols="8">
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
      </v-row>
    </v-col>
    <v-col cols="4">
      <v-card v-if="selectedStudent" class="mx-auto" max-width="400">
        <v-card-title class="text-center">
          <div class="text-center" style="width: 95%; font-size: 16px; color: #424242;">
            {{ selectedStudent.id }}
          </div>
        </v-card-title>
        <v-card-text class="text-center">
          <div style="text-align: center;">
            <img :src="getAvatarUrl(selectedStudent.id)" alt="avatar" class="avatar" style="width: 180px; height: 180px;">
            <div style="font-weight: bold; font-size: 16px; color:#1A1A1A">
              {{ selectedStudent.nameStu }}
            </div>
            <div>{{ selectedStudent.classStu }}</div>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
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
  </v-row>
</template>

<script>
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
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

.custom-table {
  padding: 16px;
  font-family: 'Kumbh Sans', sans-serif;
  color: #4F4F4F;
}

.custom-header {
  background-color: #f5f5f5; /* Puedes ajustar el color de fondo si lo deseas */
}

.custom-header-cell {
  font-weight: bold;
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
</style>
