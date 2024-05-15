<template>
  <v-card flat>
    <v-card-text
      class="black--text text-center align-center"
      style="font-size: 18px; margin-bottom: 20px; line-height: 32px;"
    >
      It is our great pleasure to have <br> you on board!
    </v-card-text>
    <v-card-text>
      <v-form>
        <v-row>
          <v-text-field
            v-model="admin"
            outlined
            placeholder="Enter the name of admin"
            type="text"
          />
        </v-row>
        <v-row>
          <v-text-field
            v-model="school"
            outlined
            placeholder="Enter the name of school"
            type="text"
          />
        </v-row>
        <v-row>
          <v-text-field
            v-model="email"
            outlined
            placeholder="Enter the school email"
            type="email"
          />
        </v-row>
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-btn
        block
        color="blue"
        elevation="0"
        click="signupUser"
        style="width: 100%; height: 50px;"
      >
        <span style="text-transform: none; color: white;">
          Next
        </span>
      </v-btn>
    </v-card-actions>
    <v-card-actions>
      <div style="display: flex; align-items: center;">
        <v-card-text style="margin-right: 0px;">
          Already have an account?
        </v-card-text>
        <router-link to="/signup" style="text-decoration: none; color: blue;">
          Signup
        </router-link>
      </div>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
}
</script>
