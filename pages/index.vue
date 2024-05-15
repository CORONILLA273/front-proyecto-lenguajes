<template>
  <Login-user />
</template>

<script>
import LoginUser from '~/components/LoginUser.vue'

export default {
  name: 'IndexPage',
  components: {
    LoginUser
  },
  layout: 'login'
}
</script>
