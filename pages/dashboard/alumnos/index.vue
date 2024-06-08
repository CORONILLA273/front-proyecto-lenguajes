<template>
  <v-app>
    <v-container>
      <v-app-bar app flat>
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
              Log Out
            </span>
          </v-btn>
        </v-toolbar>
      </v-app-bar>

      <v-row style="margin-top: -60px;">
        <template v-if="estudiantes.length === 0">
          <v-col cols="12" class="no-students-container">
            <div class="no-students-content">
              <img :src="noStudents" alt="No Students" class="no-students-image">
              <div class="no-students-text">
                No students at this time
              </div>
              <div class="no-students-subtext">
                Students will appear here after they enroll in your school.
              </div>
            </div>
          </v-col>
        </template>

        <template v-else>
          <v-col cols="1">
            <v-select
              v-model="filter"
              :items="filterOptions"
              label="Filter"
              outlined
              dense
              disabled
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
        </template>
      </v-row>

      <v-row style="">
        <template v-if="estudiantes.length > 0">
          <v-col cols="8" class="table-container">
            <v-data-table
              :headers="headers"
              :items="filteredStudents"
              elevation="0"
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
                  <td class="student-cell">
                    <div class="student-cell-content">
                      <img :src="getAvatarUrl(item.id)" alt="avatar" class="avatar">
                      <span>{{ item.nameStu }}</span>
                    </div>
                  </td>
                  <td class="student-cell">
                    {{ item.id }}
                  </td>
                  <td class="student-cell">
                    {{ item.emailStu }}
                  </td>
                  <td class="student-cell">
                    {{ item.classStu }}
                  </td>
                  <td class="student-cell">
                    {{ item.genderStu }}
                  </td>
                </tr>
              </template>
              <template #header="{ props }">
                <tr class="student-header">
                  <th v-for="header in props.headers" :key="header.text" class="student-header-cell">
                    {{ header.text }}
                  </th>
                </tr>
              </template>
            </v-data-table>
          </v-col>

          <v-col cols="4" class="card-container">
            <v-card v-if="selectedStudent" class="mx-auto" max-width="313" flat>
              <v-card-title class="text-center">
                <div class="text-center" style="width: 95%; font-size: 16px; color: #424242; font-weight: 500; font-family: 'Kumbh Sans', sans-serif;">
                  {{ selectedStudent.id }}
                </div>
              </v-card-title>
              <v-card-text class="text-center">
                <div style="text-align: center;">
                  <img :src="getAvatarUrl(selectedStudent.id)" alt="avatar" class="avatar" style="width: 180px; height: 180px; font-size: 16px;">
                  <div style="font-family: 'Kumbh Sans', sans-serif; font-weight: 700; font-size: 18px; color:#1A1A1A; padding-top: 15px; padding-bottom: 6px;">
                    {{ selectedStudent.nameStu }}
                  </div>
                  <div>{{ getTypeStudent(selectedStudent.classStu) }}</div>
                  <div class="icons" style="padding-top: 14px; padding-bottom: 30px; display: flex; justify-content: center;">
                    <div class="icon-container" @mouseenter="showTooltip('classStu')" @mouseleave="hideTooltip">
                      <img :src="teacherIcon" alt="Teacher" class="icon">
                      <div v-if="tooltipVisible && tooltipType === 'classStu'" class="tooltip">
                        {{ selectedStudent.classStu }}
                      </div>
                    </div>
                    <div class="icon-container" @mouseenter="showTooltip('phoneStu')" @mouseleave="hideTooltip">
                      <img :src="callCallingIcon" alt="Call Calling" class="icon">
                      <div v-if="tooltipVisible && tooltipType === 'phoneStu'" class="tooltip">
                        {{ selectedStudent.phoneStu }}
                      </div>
                    </div>
                    <div class="icon-container" @mouseenter="showTooltip('emailStu')" @mouseleave="hideTooltip">
                      <img :src="smsIcon" alt="SMS" class="icon">
                      <div v-if="tooltipVisible && tooltipType === 'emailStu'" class="tooltip">
                        {{ selectedStudent.emailStu }}
                      </div>
                    </div>
                  </div>
                  <div class="about-section">
                    About
                  </div>
                  <div style="text-align: justify;">
                    Lorem ipsum dolor sit amet consectetur, adipisicing elit. Repellendus officiis obcaecati fugiat dolorem dicta adipisci natus dignissimos officia unde sequi reprehenderit ipsum expedita omnis, nihil vitae architecto nulla cum eaque?
                  </div>
                  <div class="info-section">
                    <div class="info-item">
                      <div class="info-label" style="font-weight: 600;">
                        Age
                      </div>
                      <div style="font-size: 14px; font-weight: 500;">
                        21
                      </div>
                    </div>
                    <div class="info-item">
                      <div class="info-label" style="font-weight: 600;">
                        Gender
                      </div>
                      <div>{{ selectedStudent.genderStu }}</div>
                    </div>
                  </div>
                  <div class="about-section">
                    People from the same class
                  </div>
                  <div class="same-class">
                    <div class="avatars">
                      <img
                        v-for="(student, index) in firstFiveClassmates"
                        :key="student.id"
                        :src="getAvatarUrl(student.id)"
                        alt="avatar"
                        class="avatar-small"
                        :style="{ zIndex: index }"
                      >
                    </div>
                    <div v-if="remainingClassmatesCount > 0" class="extra-count">
                      +{{ remainingClassmatesCount }} more
                    </div>
                  </div>
                </div>
              </v-card-text>
            </v-card>
          </v-col>
        </template>
      </v-row>

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
                    &nbsp;
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
                    Add Student
                  </span>
                </v-btn>
              </v-col>
            </v-row>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-container>
  </v-app>
</template>

<script>
import noStudents from '../../../assets/estudiantes/no-notification.png'
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

      juan: [],

      tooltipVisible: false,
      tooltipType: null,

      callCallingIcon,
      smsIcon,
      teacherIcon,
      noStudents,

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
    },
    filteredClassmates () {
      if (!this.selectedStudent) { return [] }
      return this.estudiantes.filter(student => student.classStu === this.selectedStudent.classStu && student.id !== this.selectedStudent.id)
    },
    firstFiveClassmates () {
      return this.filteredClassmates.slice(0, 5)
    },
    remainingClassmatesCount () {
      return this.filteredClassmates.length - 5
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
    getTypeStudent (classStu) {
      if (classStu === 'SS 1' || classStu === 'SS 2' || classStu === 'SS 3') {
        return 'Science Student'
      } else if (classStu === 'JSS 1' || classStu === 'JSS 2' || classStu === 'JSS 3') {
        return 'Math Student'
      } else if (classStu === 'SJ 1' || classStu === 'SJ 2' || classStu === 'SJ 3') {
        return 'Physics Student'
      } else {
        return 'Medical Student'
      }
    },
    showTooltip (type) {
      this.tooltipType = type
      this.tooltipVisible = true
    },
    hideTooltip () {
      this.tooltipVisible = false
      this.tooltipType = null
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
.student-table {
  font-weight: 500;
  padding: 16px;
  font-family: 'Kumbh Sans', sans-serif;
  color: #4F4F4F;
}

.v-app-bar {
  background-color: white !important;
}

.student-header {
  background-color: #f5f5f5;
}

.student-header-cell {
  font-weight: 700;
  padding: 16px;
  text-align: left;
  font-size: 14px;
  color: #4F4F4F;
}

.student-cell {
  color: #4F4F4F;
}

.student-cell-content {
  display: flex;
  align-items: center;
}

.avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  margin-right: 8px;
}

.avatar-small {
  width: 37px;
  height: 37px;
  border-radius: 50%;
  margin-right: -8px;
  position: relative;
}

.cell-text {
  color: inherit;
}

.row-hover {
  background-color: #D5E7F6 !important;
}

.row-selected {
  background-color: #509CDB !important;
  color: white !important;
}

.row-selected .student-cell,
.row-selected .student-cell .cell-text {
  color: white !important;
}

.v-data-table tbody tr {
  cursor: pointer;
  color: #4F4F4F;
  height: 55px;
  line-height: 55px;
}

.icons {
  margin-top: 16px;
}

.icon {
  width: 50px;
  height: 50px;
  margin: 0 8px;
  padding: 10px;
}

.icon-container {
  position: relative;
}

.tooltip {
  position: absolute;
  font-family: 'Kumbh Sans', sans-serif;
  color: #4F4F4F;
  padding: 5px;
  top: 60px;
  left: 50%;
  transform: translateX(-50%);
  white-space: nowrap;
  z-index: 10;
}

.about-section {
  font-family: 'Kumbh Sans', sans-serif;
  color: black;
  font-weight: bold;
  font-size: 12px;
  text-align: left;
  margin: 12px 0;
}

.info-section {
  display: flex;
  justify-content: space-between;
  margin: 16px 0;
  text-align: left;
  font-family: 'Kumbh Sans', sans-serif;
}

.info-item {
  width: 50%;
  font-family: 'Kumbh Sans', sans-serif;
}

.info-label {
  font-family: 'Kumbh Sans', sans-serif;
  font-weight: 600;
  font-size: 12px;
  padding-bottom: 3px;
  color: #1A1A1A;
}

.same-class {
  display: flex;
  align-items: center;
}

.avatars {
  display: flex;
  position: relative;
}

.extra-count {
  margin-left: 20px;
  font-size: 10px;
  color: #73B0E2;
}

.table-container {
  margin-right: 0px;
}

.card-container {
  margin-left: 0px;
}

.no-students-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 400px;
  text-align: center;
}

.no-students-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.no-students-image {
  width: 380px;
  margin-bottom: 16px;
}

.no-students-text {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 28px;
  font-weight: 600;
  color: #4F4F4F;
  margin-bottom: 8px;
}

.no-students-subtext {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 14px;
  font-weight: 500;
  color: #4F4F4F;
}

.v-toolbar {
  background-color: white;
}
</style>
