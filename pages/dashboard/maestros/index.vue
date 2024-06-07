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
        style="width: 1085px !important;"
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
                <span>{{ item.nameTea }}</span>
              </div>
            </td>
            <td class="custom-cell">
              {{ item.subjectTea }}
            </td>
            <td class="custom-cell">
              {{ item.classTea }}
            </td>
            <td class="custom-cell">
              {{ item.emailTea }}
            </td>
            <td class="custom-cell">
              {{ item.genderTea }}
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
      hoveredRow: null,
      selectedRow: null,
      selectedStudent: null,

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
    selectRow (teacher) {
      this.selectedRow = teacher.id
      this.selectedStudent = teacher
      this.hoveredRow = null
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
