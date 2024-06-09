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
              Add Teachers
            </span>
          </v-btn>
          <v-spacer />
          <v-icon left>
            mdi-bell
          </v-icon>
          <v-btn text color="blue" style="text-align: right; margin-right: 50px;" @click="logOut()">
            <span style="color: black; text-transform: none;">
              Log Out
            </span>
          </v-btn>
        </v-toolbar>
      </v-app-bar>

      <v-row style="margin-top: -60px;">
        <template v-if="maestros.length === 0">
          <v-col cols="12" class="no-teachers-container">
            <div class="no-teachers-content">
              <img :src="noTeachers" alt="No Teachers" class="no-teachers-image">
              <div class="no-teachers-text">
                No teachers at this time
              </div>
              <div class="no-teachers-subtext">
                Teachers will appear here after they enroll in your school.
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
            />
          </v-col>
          <v-col cols="6">
            <v-text-field
              v-model="searchTeacher"
              prepend-inner-icon="mdi-magnify"
              label="Search for a teacher by name or email"
              outlined
              hide-details
              @input="searchTeacherByName"
            />
          </v-col>
        </template>
      </v-row>

      <v-col cols="12">
        <v-row v-if="!selectedTeacher && maestros.length > 0" class="mt-3">
          <v-data-table
            :headers="headers"
            :items="filteredTeachers"
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

        <v-row v-if="selectedTeacher" class="mt-3 teacher-details">
          <v-container>
            <v-layout justify-center>
              <v-flex xs12 sm10 md15 lg10>
                <v-card class="pa-5" elevation="0">
                  <v-row>
                    <v-col cols="6" class="text-center" style="padding-right: 20px;">
                      <img :src="getAvatarUrl(selectedTeacher.id)" alt="avatar" class="avatar-large">
                      <div class="teacher-name">
                        {{ selectedTeacher.nameTea || 'No name available' }}
                      </div>
                      <div class="teacher-class">
                        {{ selectedTeacher.subjectTea || 'No class specified' }}
                      </div>
                      <div class="icons" style="padding-top: 14px; padding-bottom: 30px; display: flex; justify-content: center;">
                        <div class="icon-container" @mouseenter="showTooltip('classTea')" @mouseleave="hideTooltip">
                          <img :src="teacherIcon" alt="Teacher" class="icon">
                          <div v-if="tooltipVisible && tooltipType === 'classTea'" class="tooltip">
                            {{ selectedTeacher.classTea }}
                          </div>
                        </div>
                        <div class="icon-container" @mouseenter="showTooltip('phoneTea')" @mouseleave="hideTooltip">
                          <img :src="callCallingIcon" alt="Call Calling" class="icon">
                          <div v-if="tooltipVisible && tooltipType === 'phoneTea'" class="tooltip">
                            {{ selectedTeacher.phoneTea }}
                          </div>
                        </div>
                        <div class="icon-container" @mouseenter="showTooltip('emailTea')" @mouseleave="hideTooltip">
                          <img :src="smsIcon" alt="SMS" class="icon">
                          <div v-if="tooltipVisible && tooltipType === 'emailTea'" class="tooltip">
                            {{ selectedTeacher.emailTea }}
                          </div>
                        </div>
                      </div>
                    </v-col>
                    <v-col cols="6" style="padding-left: 50px;">
                      <div class="about-section">
                        <h3>About</h3>
                        <p class="about-text">
                          Nulla Lorem mollit cupidatat irure. Laborum magna nulla duis ullamco cillum dolor. Voluptate exercitation incididunt aliquip deserunt reprehenderit elit laborum. Nulla Lorem mollit cupidatat irure. Laborum magna nulla duis ullamco cillum dolor. Voluptate exercitation incididunt aliquip deserunt reprehenderit elit laborum.
                        </p>
                      </div>
                      <div class="info-section">
                        <v-row>
                          <v-col cols="6">
                            <div class="info-label">
                              Age
                            </div>
                            <div class="about-text">
                              37
                            </div>
                          </v-col>
                          <v-col cols="6">
                            <div class="info-label">
                              Gender
                            </div>
                            <div class="about-text">
                              {{ selectedTeacher.genderTea || 'No gender specified' }}
                            </div>
                          </v-col>
                        </v-row>
                      </div>
                      <div class="about-section" style="padding-bottom: 28px;">
                        <h3>People from the same class</h3>
                      </div>
                      <div class="same-class">
                        <div class="avatars">
                          <img
                            v-for="(teacher, index) in firstFiveMates"
                            :key="teacher.id"
                            :src="getAvatarUrl(teacher.id)"
                            alt="avatar"
                            class="avatar-small"
                            :style="{ zIndex: index }"
                          >
                        </div>
                        <div v-if="remainingMatesCount > 0" class="extra-count">
                          +{{ remainingMatesCount }} more
                        </div>
                      </div>
                    </v-col>
                  </v-row>
                </v-card>
              </v-flex>
            </v-layout>
          </v-container>
        </v-row>

        <v-dialog v-model="showNuevo" max-width="1100" persistent @click:outside="closeDialog">
          <v-card style="overflow: hidden; width: 100%; height: 90vh; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 50px;">
            <v-card-title class="text-h4" style="text-align: left; width: 100%;">
              &nbsp;&nbsp;Add Teachers
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
                        v-model="teacherName"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        type="text"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                    <v-col cols="4">
                      Email
                      <v-text-field
                        v-model="emailTeacher"
                        :rules="emailValidation"
                        outlined
                        placeholder="Email"
                        type="email"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                    <v-col cols="4">
                      Phone Number
                      <v-text-field
                        v-model="phoneNumberTeacher"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        placeholder="Phone Number"
                        type="text"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                  </v-row>
                  <v-row>
                    <v-col cols="4">
                      Password
                      <v-text-field
                        v-model="passwordTeacher"
                        :rules="passwordValidation"
                        outlined
                        type="password"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                    <v-col cols="4">
                      Class
                      <v-select
                        v-model="classNameTeacher"
                        :items="['JSS 1', 'JSS 2', 'JSS 3', 'SS 1', 'SS 2', 'SS 3']"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        label="Class"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                    <v-col cols="4">
                      Subject
                      <v-text-field
                        v-model="subjectTeacher"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        placeholder="Subject"
                        type="text"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                  </v-row>
                  <v-row>
                    <v-col cols="4">
                      Gender
                      <v-select
                        v-model="genderNameTeacher"
                        :items="['Male', 'Female', 'Other']"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        label="Gender"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                    <v-col cols="4">
                      Designation
                      <v-text-field
                        v-model="designationTeacher"
                        :rules="[v => !!v || 'Field is required']"
                        outlined
                        placeholder="Designation"
                        type="text"
                        style="margin-bottom: 20px;"
                      />
                    </v-col>
                  </v-row>
                </v-container>
              </v-form>
            </v-card-text>

            <v-card-actions style="width: 100%; display: flex; justify-content: center; margin-top: -50px;">
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
                      Add Teacher
                    </span>
                  </v-btn>
                </v-col>
              </v-row>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-container>
  </v-app>
</template>

<script>
import noTeachers from '../../../assets/estudiantes/no-notification.png'
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
          value: 'nameTea'
        },
        {
          text: 'Subject',
          align: 'left',
          sortable: true,
          value: 'subjectTea'
        },
        {
          text: 'Class',
          align: 'left',
          sortable: true,
          value: 'classTea'
        },
        {
          text: 'Email Address',
          align: 'left',
          sortable: true,
          value: 'emailTea'
        },
        {
          text: 'Gender',
          align: 'left',
          sortable: true,
          value: 'genderTea'
        }
      ],
      token: null,
      maestros: [],
      juan: [],
      search: '',
      showNuevo: false,
      validForm: false,
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
      selectedTeacher: null,
      searchTeacher: '',
      filter: null,
      filterOptions: ['Option1', 'Option2'],

      callCallingIcon,
      smsIcon,
      teacherIcon,
      noTeachers,

      tooltipVisible: false,
      tooltipType: null,

      passwordValidation: [
        v => (v && v.length > 8) || 'Password must have be more than 8 chars'
      ],
      emailValidation: [
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ]
    }
  },
  computed: {
    filteredTeachers () {
      const searchTerm = this.searchTeacher.toLowerCase()
      return this.maestros.filter((teacher) => {
        return (
          teacher.nameTea.toLowerCase().includes(searchTerm) ||
          teacher.emailTea.toLowerCase().includes(searchTerm)
        )
      })
    },
    filteredMates () {
      if (!this.selectedTeacher) { return [] }
      return this.maestros.filter(teacher => teacher.classTea === this.selectedTeacher.classTea && teacher.id !== this.selectedTeacher.id)
    },
    firstFiveMates () {
      return this.filteredMates.slice(0, 5)
    },
    remainingMatesCount () {
      return this.filteredMates.length - 5
    }
  },
  mounted () {
    this.token = localStorage.getItem('token')
    if (!this.token) {
      this.$router.push('/')
    }
    this.getAllTeachers()
  },
  methods: {
    logOut () {
      this.token = localStorage.removeItem('token')
      this.$router.push('/')
    },
    getAllTeachers () {
      const url = '/api/auth/get-all-teachers'
      const config = {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      }
      this.$axios.get(url, config)
        .then((res) => {
          if (res.data.message === 'Success') {
            this.maestros = res.data.teachers
          } else if (res.data.message === 'Invalid Token') {
            this.$router.push('/')
          }
        })
        .catch((err) => {
          console.log(err)
          this.$router.push('/')
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
      this.selectedTeacher = teacher
      this.hoveredRow = null
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
          nameTea: this.teacherName,
          emailTea: this.emailTeacher,
          phoneTea: this.phoneNumberTeacher,
          passwordTea: this.passwordTeacher,
          classTea: this.classNameTeacher,
          subjectTea: this.subjectTeacher,
          genderTea: this.genderNameTeacher,
          designationTea: this.designationTeacher
        }
        const config = {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
        const url = '/api/auth/registrar-profesor'
        this.$axios.post(url, sendData, config)
          .then((res) => {
            if (res.data.message === 'Profesor Registrado Satisfactoriamente') {
              this.getAllTeachers()
              this.showNuevo = false
              this.resetForm()
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
          nameTea: this.teacherName,
          emailTea: this.emailTeacher,
          phoneTea: this.phoneNumberTeacher,
          passwordTea: this.passwordTeacher,
          classTea: this.classNameTeacher,
          subjectTea: this.subjectTeacher,
          genderTea: this.genderNameTeacher,
          designationTea: this.designationTeacher
        }
        const config = {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
        const url = '/api/auth/registrar-profesor'
        this.$axios.post(url, sendData, config)
          .then((res) => {
            if (res.data.message === 'Profesor Registrado Satisfactoriamente') {
              this.getAllTeachers()
              this.resetForm()
            }
          })
          .catch((err) => {
            console.log(err)
          })
      } else {
        alert('Faltan Datos')
      }
    },
    resetForm () {
      // Resetear valores de los campos del formulario
      this.teacherName = ''
      this.emailTeacher = ''
      this.phoneNumberTeacher = ''
      this.passwordTeacher = ''
      this.classNameTeacher = null // Asegurarse de que los v-select también se resetean correctamente
      this.subjectTeacher = ''
      this.genderNameTeacher = null // Asegurarse de que los v-select también se resetean correctamente
      this.designationTeacher = ''
    },
    searchTeacherByName () {
      const teacher = this.maestros.find(m => m.nameTea.toLowerCase() === this.searchTeacher.toLowerCase())
      if (teacher) {
        this.selectedTeacher = teacher
      } else {
        this.selectedTeacher = null
      }
    },
    clearSearch () {
      this.searchTeacher = ''
      this.selectedTeacher = null
    },
    closeDialog () {
      this.showNuevo = false
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

.about-text {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 21px;
  text-align: left;
  color: #A7A7A7;
}

.custom-table {
  padding: 16px;
  font-family: 'Kumbh Sans', sans-serif;
  color: #4F4F4F;
}

.custom-header {
  background-color: #f5f5f5;
}

.custom-header-cell {
  font-weight: bold;
  padding: 16px;
  text-align: left;
  font-size: 14px;
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
  color: inherit;
}

.row-hover {
  background-color: #D5E7F6 !important;
}

.row-selected {
  background-color: #509CDB !important;
  color: white !important;
}

.row-selected .custom-cell,
.row-selected .custom-cell .cell-text {
  color: white !important;
}

.v-data-table tbody tr {
  cursor: pointer;
  color: #4F4F4F;
  height: 55px;
  line-height: 55px;
}

.fixed-width {
  width: 100%;
}

.mt-3 {
  margin-top: 16px;
}

.teacher-details {
  display: flex;
  justify-content: center;
  align-items: center;
}

.avatar-large {
  width: 290px;
  height: 290px;
  border-radius: 50%;
}

.teacher-name {
  font-weight: 700;
  font-size: 16px;
  color: #1A1A1A;
  padding-top: 15px;
  padding-bottom: 6px;
}

.teacher-class {
  font-size: 14px;
  color: #4F4F4F;
}

.icons {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.icon {
  margin: 0 10px;
  width: 30px;
  height: 30px;
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
  margin-top: 20px;
}

.info-section {
  margin-top: 20px;
}

.info-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.info-label {
  font-weight: bold;
  color: #4F4F4F;
}

.v-toolbar {
  background-color: white !important;
}

.same-class {
  display: flex;
  align-items: center;
}

.avatars {
  display: flex;
  position: relative;
}

.avatar-small {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  margin-right: -20px;
  position: relative;
}

.extra-count {
  margin-left: 20px;
  font-size: 10px;
  color: #73B0E2;
}

.no-teachers-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 400px;
  text-align: center;
}

.no-teachers-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.no-teachers-image {
  width: 380px;
  margin-bottom: 16px;
}

.no-teachers-text {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 28px;
  font-weight: 600;
  color: #4F4F4F;
  margin-bottom: 8px;
}

.no-teachers-subtext {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 14px;
  font-weight: 500;
  color: #4F4F4F;
}
</style>
