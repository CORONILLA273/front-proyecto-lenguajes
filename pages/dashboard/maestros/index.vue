<template>
  <v-col cols="12">
    <v-row>
      <v-btn block color="blue">
        <span style="color: white; text-transform: none;">
          Add Teachers
        </span>
      </v-btn>
    </v-row>
  </v-col>
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
