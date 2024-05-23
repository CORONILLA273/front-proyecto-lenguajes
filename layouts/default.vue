<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      color="#152259"
      :permanent="$vuetify.breakpoint.lgAndUp"
      :temporary="$vuetify.breakpoint.mdAndDown"
      style="width: 242px; height: 100vh; left: 1px"
    >
      <v-list dense>
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
              <v-list-item-title style="width: Hug(160px); height: Hug(17px); top: 10px; gap: 16px" class="text-center d-flex flex-column align-center white--text">
                <span style="font-family: Kumbh Sans; font-size: 14px; font-weight: 600; line-height: 17.36px; text-align: left; width: 131px; height: 17px">Udemy Int. School</span>
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item-content>
        </v-list-item>
        <v-list-item
          v-for="(item) in items"
          :key="item.id"
          :to="item.to"
          router
          exact
          :class="{'list-item-hover': true, 'list-item-active': $route.path === item.to}"
          style="width: 242px; height: 40px;padding: 4px 12px; border-radius: 12px; display: flex; align-items: center; justify-content: space-between;"
          @click="item.to ? null : handleItem(item)"
        >
          <v-list-item-action style="margin-right: 12px; margin-left: 25%; padding: 4px; display: flex; justify-content: center; align-items: center; object-fit: contain;">
            <v-img :src="item.icon" style="width: 15px; height: 15px; object-fit: contain;" />
          </v-list-item-action>
          <v-list-item-content style="width: 100%; display: flex; align-items: center; justify-content: center;">
            <v-list-item-title style="font-family: Kumbh Sans; font-size: 12px; font-weight: 600; line-height: 17.36px; text-align: left; width: 72px; height: 17px" class="white--text">
              {{ item.title }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item
          v-for="(item) in items2"
          :key="item.id"
          :to="item.to"
          router
          exact
          :class="{'list-item-hover': true, 'list-item-active': $route.path === item.to}"
          style="width: 242px; height: 40px;padding: 4px 12px; border-radius: 12px; top: 100px; display: flex; align-items: center; justify-content: space-between;"
          @click="item.to ? null : handleItem(item)"
        >
          <v-list-item-action style="margin-right: 12px; margin-left: 25%; padding: 4px; display: flex; justify-content: center; align-items: center; object-fit: contain;">
            <v-img :src="item.icon" style="width: 15px; height: 15px; object-fit: contain;" />
          </v-list-item-action>
          <v-list-item-title style="font-family: Kumbh Sans; font-size: 12px; font-weight: 600; line-height: 17.36px; text-align: left; width: 72px; height: 17px" class="white--text">
            {{ item.title }}
          </v-list-item-title>
          <v-chip v-if="item.new" color="#B9D7F1" style="width: 100px; height: 14px; left: 0px;  gap: 10px; border-radius: 8px; opacity: 0px;">
            <span style="font-family: Kumbh Sans; font-size: 10px; font-weight: 600; line-height: 12.4px; text-align: left;">NEW</span>
          </v-chip>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar v-show="$vuetify.breakpoint.mdAndDown" app>
      <v-app-bar-nav-icon
        @click.stop="drawer = !drawer"
      />
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
          id: 1,
          icon: require('~/assets/sideBar/home-2.png'),
          title: 'Dashboard',
          to: '/dashboard'
        },
        {
          id: 2,
          icon: require('~/assets/sideBar/home-2.png'),
          title: 'Teachers',
          to: '/dashboard/maestros'
        },
        {
          id: 3,
          icon: require('~/assets/sideBar/school.png'),
          title: 'Students/ Classes',
          to: '/dashboard/alumnos'
        },
        {
          id: 4,
          icon: require('~/assets/sideBar/Billing.png'),
          title: 'Billing'
        },
        {
          id: 5,
          icon: require('~/assets/sideBar/Settings.png'),
          title: 'Settings and profile'
        },
        {
          id: 6,
          icon: require('~/assets/sideBar/Exams.png'),
          title: 'Exams'
        }
      ],
      items2: [
        {
          id: 7,
          icon: require('~/assets/sideBar/Billing.png'),
          title: 'Features',
          new: true
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false
    }
  },
  methods: {
    handleItem (item) {
      if (!item.to) {
        //
      }
    }
  }
}
</script>

<style>

@media (max-width: 960px) {
  .list-item-hover:hover, .list-item-active {
    width: 100%; /* Adaptar la anchura al 100% para dispositivos pequeños */
  }
}

/* Estilos para dispositivos medianos */
@media (min-width: 961px) and (max-width: 1264px) {
  .list-item-hover:hover, .list-item-active {
    width: 150px; /* Anchura intermedia para tablets */
  }
}

.list-item-hover:hover {
  background-color: #509CDB;
  width: 200px;
}
.list-item-active {
  background-color: #509CDB; /* Color para ítem activo */
  color: white;
  width: 200px;
}
.new {
  font-family: Kumbh Sans;
  font-size: 10px;
  font-weight: 600;
  line-height: 12.4px;
  text-align: left;
  background: #000000;
}
</style>
