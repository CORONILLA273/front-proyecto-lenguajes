<template>
  <v-app>
    <v-main>
      <v-card-title style="font-size: 30px; margin-bottom: 30px">
        Dashboard
      </v-card-title>
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
