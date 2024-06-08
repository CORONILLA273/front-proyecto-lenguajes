<template>
  <v-app>
    <v-container>
      <v-app-bar app flat style="height: 100px;">
        <v-toolbar flat class="custom-toolbar" style="margin-top: 50px;">
          <div class="toolbar-content">
            <p style="margin-left: 150px">
              Learn how to launch faster <br>
              Watch our webinar for tips from our experts and get a limited timer offer
            </p>
            <v-spacer />
            <v-icon style="margin-right: 50px">
              mdi-bell
            </v-icon>
            <v-btn color="blue" style="text-align: right; margin-right: 100px; width: 130px; height: 50px; border-radius: 10px;" @click="logOut()">
              <span style="color: white; text-transform: none; font-size: 15px;">
                Log out
              </span>
            </v-btn>
          </div>
        </v-toolbar>
      </v-app-bar>

      <h1 style="display: flex; justify-content: center;">
        Welcome to your dashboard, Udemy school
      </h1>
      <br>
      <h2 style="display: flex; justify-content: center;">
        Uyo/school/@teachable.com
      </h2>

      <v-card flat style="margin-top: 50px;">
        <v-card flat class="mt-4 d-flex" style="display: flex; justify-content: center;">
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
        <v-card flat class="mt-4 d-flex" style="display: flex; justify-content: center;">
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
        <v-card flat class="mt-4 d-flex" style="display: flex; justify-content: center;">
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
        <v-row>
          <v-col class="d-flex justify-end">
            <v-btn style="background-color: #152259; color: white; border-radius: 200px; margin-right: 150px; height: 70px; width: 230px;">
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
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {
  mounted () {
    const token = localStorage.getItem('token')
    if (!token) {
      this.$router.push('/')
    }
  },
  methods: {
    logOut () {
      this.token = localStorage.removeItem('token')
      this.$router.push('/')
    }
  }
}
</script>

<style>
.v-toolbar {
  background-color: #f5f5f5 !important;
}

.custom-toolbar {
  height: 100px; /* Ajusta la altura según tus necesidades */
}

.toolbar-content {
  display: flex;
  align-items: center;
  width: 100%;
}

custom-button2 {
  background-color: #00008B !important;
  color: white !important;
  width: 250px;
  height: 80px !important; /* Asegúrate de que !important esté aplicado */
  font-size: 20px;
  border-radius: 300px;
}
</style>
