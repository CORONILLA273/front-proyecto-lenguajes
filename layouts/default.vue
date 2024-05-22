<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      color="#152259"
      permanent
      style="width: 250px; height: 789px; left: 1px"
    >
      <v-list>
        <v-list-item>
          <v-list-item-content class="justify-center">
            <v-list-item-title class="text-h6 text-center d-flex flex-column align-center">
              <img
                src="~/assets/sideBar/Ellipse 6.png"
                class="rounded-circle"
                aspect-ratio="1"
                width="65px"
                height="65px"
                top="26px"
                left="88px"
              >
            </v-list-item-title>
            <v-list-item-content style="width: 192px; height: 40px; top: 103px; left: 25px; padding: 8px" class="justify-center">
              <v-list-item-title style="width: Hug(131px); height: Hug(17px); top: 10px; gap: 16px" class="text-center d-flex flex-column align-center white--text">
                <span style="font-family: Kumbh Sans; font-size: 14px; font-weight: 600; line-height: 17.36px; text-align: left; width: 131px; height: 17px">Udemy Int. School</span>
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item-content>
        </v-list-item>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
          style="width: 192px; height: 40px; padding:4px; display: flex; align-items: center; justify-content: center;"
        >
          <v-list-item-action style="margin-right: 4px; margin-left: 25%; display: flex; justify-content: center; align-items: center;">
            <v-img :src="item.icon" style="width: 24px; height: 24px;" />
          </v-list-item-action>
          <v-list-item-content style="width: 100%; display: flex; align-items: center; justify-content: center;">
            <v-list-item-title style="font-family: Kumbh Sans; font-size: 14px; font-weight: 600; line-height: 17.36px; text-align: center; width: 72px; height: 17px" class="white--text">
              {{ item.title }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>{{ title }}</v-toolbar-title>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [
        {
          icon: require('~/assets/sideBar/home-2.png'),
          title: 'Dashboard',
          to: '/dashboard'
        },
        {
          icon: require('~/assets/sideBar/home-2.png'),
          title: 'Teachers',
          to: '/dashboard/maestros'
        },
        {
          icon: require('~/assets/sideBar/school.png'),
          title: 'Students/ Classes',
          to: '/dashboard/maestros'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>
