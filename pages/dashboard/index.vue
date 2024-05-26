<template>
  <v-app>
    <v-main>
      <v-container>
        <v-card flat class="mb-4 d-flex align-center justify-space-between">
          <v-card-text class="black-text principal-text">
            Learn how to launch faster <br>
            watch our webinar for tips from our experts and get a limited timer offer
          </v-card-text>
          <v-icon class="mx-6">
            mdi-bell
          </v-icon>
          <v-btn class="custom-button">
            Log Out
          </v-btn>
        </v-card>
        <v-card flat>
          <v-card-title class="d-flex justify-center title-text">
            Welcome to your dashboard, Udemy school
          </v-card-title>
          <v-card-subtitle class="text-center black-text subtitle-text">
            Uyo/school/@teachable.com
          </v-card-subtitle>
          <v-card flat class="mt-4 d-flex">
            <div class="icon-container">
              <v-icon size="48px">
                mdi-account-plus
              </v-icon>
            </div>
            <div class="text-container">
              <v-card-title>Add other admins</v-card-title>
              <v-card-text class="black-text">
                Create rich course content and coaching products for your students. <br>
                When you give them a pricing plan, they'll appear on your site!
              </v-card-text>
            </div>
          </v-card>
          <v-card flat class="mt-4 d-flex">
            <div class="icon-container">
              <v-icon size="48px">
                mdi-library
              </v-icon>
            </div>
            <div class="text-container">
              <v-card-title>Add classes</v-card-title>
              <v-card-text class="black-text">
                Create rich course content and coaching products for your students. <br>
                When you give them a pricing plan, they'll appear on your site!
              </v-card-text>
            </div>
          </v-card>
          <v-card flat class="mt-4 d-flex">
            <div class="icon-container">
              <v-icon size="48px">
                mdi-school
              </v-icon>
            </div>
            <div class="text-container">
              <v-card-title>Add students</v-card-title>
              <v-card-text class="black-text">
                Create rich course content and coaching products for your students. <br>
                When you give them a pricing plan, they'll appear on your site!
              </v-card-text>
            </div>
          </v-card>
        </v-card>
        <v-row>
          <v-col class="d-flex justify-end">
            <v-btn class="custom-button custom-button2">
              <v-icon left>
                mdi-headphones
              </v-icon>
              Support
              <v-icon right>
                mdi-chevron-up
              </v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  mounted () {
    const token = localStorage.getItem('token')
    if (!token) {
      this.$router.push('/')
    }
  }
}
</script>

<style>
.container {
  margin-top: -40px;
}
.mb-4 {
  margin-bottom: 16px;
}
.flex-grow-1 {
  flex-grow: 1;
}
.custom-button {
  background-color: #5564eb !important;
  color: white !important;
}

.custom-button2 {
  background-color: #00008B !important;
  color: white !important;
  width: 250px;
  height: 80px !important; /* Asegúrate de que !important esté aplicado */
  font-size: 20px;
  border-radius: 300px;
}

.mx-6 {
  margin-left: 24px;
  margin-right: 24px;
}
.mt-4 {
  margin-top: 16px;
}

.title-text {
  font-size: 30px;
}

.subtitle-text {
  font-size: 20px;
}

.principal-text {
  font-size: 15px;
}

.black-text {
  color: black !important;
}
.icon-container {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}
.text-container {
  flex: 9;
}
</style>
