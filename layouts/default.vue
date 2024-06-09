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
        <template>
          <v-list dense>
            <v-list-item-group>
              <template v-for="item in items">
                <div :key="'div-' + item.id" style="width: 242px; margin-bottom: 8px;">
                  <v-list-item
                    :key="item.id"
                    :to="item.to"
                    router
                    exact
                    :class="['list-item', {'list-item-hover': true, 'list-item-active': $route.path === item.to}]"
                    @mouseover="item.hover = true"
                    @mouseleave="item.hover = false"
                    @click="toggleSubItems(item)"
                  >
                    <v-list-item-action style="margin-right: 12px; margin-left: 16px; padding: 4px; display: flex; justify-content: center; align-items: center; object-fit: contain;">
                      <v-img :src="item.icon" class="item-icon" />
                    </v-list-item-action>
                    <v-list-item-content>
                      <v-list-item-title class="white--text item-title">
                        {{ item.title }}
                      </v-list-item-title>
                    </v-list-item-content>
                    <v-list-item-action v-if="item.subItems && item.subItems.length">
                      <v-icon
                        v-show="item.hover || item.visible"
                        :style="{ transform: item.rotated ? 'rotate(90deg)' : 'rotate(0deg)' }"
                        color="white"
                      >
                        mdi-chevron-right
                      </v-icon>
                    </v-list-item-action>
                  </v-list-item>

                  <!-- SubItems List -->
                  <v-list v-if="item.visible && item.subItems" dense class="sub-item-list">
                    <v-list-item
                      v-for="subItem in item.subItems"
                      :key="subItem.id"
                      :to="subItem.to"
                      :class="['sub-item-list ', {'list-item-hover': true, 'list-item-active': $route.path === subItem.to}]"
                      style="margin: 0; height: 40px;"
                    >
                      <v-list-item-action>
                        <v-icon style="margin-left: 16px; display: flex; justify-content: center; align-items: center; object-fit: contain;" color="white">
                          mdi-chevron-right
                        </v-icon>
                      </v-list-item-action>
                      <v-list-item-content>
                        <v-list-item-title class="white--text sub-item-title">
                          {{ subItem.title }}
                        </v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list>
                </div>
              </template>
            </v-list-item-group>
          </v-list>
        </template>

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
          <v-list-item-action style="margin-right: 12px; margin-left: 16px; padding: 4px; display: flex; justify-content: center; align-items: center; object-fit: contain;">
            <v-img :src="item.icon" style="width: 15px; height: 15px; object-fit: contain;" />
          </v-list-item-action>
          <v-list-item-title style="margin-left: 4%; font-family: Kumbh Sans; font-size: 12px; font-weight: 600; line-height: 17.36px; text-align: left;" class="white--text">
            {{ item.title }}
          </v-list-item-title>
          <v-chip v-if="item.new" color="#B9D7F1" style=" width: 65%; margin-right: 25px; height: 14px; border-radius: 8px; font-family: Kumbh Sans; font-size: 10px; font-weight: 600; line-height: 12.4px; text-align: right; padding: 0 4px; justify-content: center;">
            NEW
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
      drawer: false,
      fixed: false,
      items: [
        {
          id: 1,
          icon: require('~/assets/sideBar/home-2.png'),
          title: 'Dashboard',
          to: '/dashboard',
          hover: false
        },
        {
          id: 2,
          icon: require('~/assets/sideBar/home-2.png'),
          title: 'Teachers',
          hover: false,
          visible: false,
          rotated: false,
          subItems: [
            {
              id: 14,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'All teachers',
              new: true,
              to: '/dashboard/maestros'
            },
            {
              id: 15,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Add Teachers'
            },
            {
              id: 16,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Teachers Details'
            }
          ]
        },
        {
          id: 3,
          icon: require('~/assets/sideBar/school.png'),
          title: 'Students/ Classes',
          hover: true,
          visible: false,
          rotated: false,
          subItems: [
            {
              id: 14,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'All Students',
              new: true,
              to: '/dashboard/alumnos'
            },
            {
              id: 15,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Admission Form',
              to: '/dashboard/alumnos/admissionForms'
            },
            {
              id: 16,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Student Promotion',
              to: '/dashboard/alumnos/studentPromotion'
            },
            {
              id: 17,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Class',
              to: '/dashboard/alumnos/class'
            }
          ]
        },
        {
          id: 4,
          icon: require('~/assets/sideBar/Billing.png'),
          title: 'Billing',
          hover: false,
          visible: false,
          rotated: false,
          subItems: [
            {
              id: 10,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Student Billing',
              new: true
            },
            {
              id: 11,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Parent Billing'
            },
            {
              id: 12,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'School Billing'
            },
            {
              id: 13,
              icon: require('~/assets/sideBar/vector.png'),
              title: 'Friends Billing'
            }
          ]
        },
        {
          id: 5,
          icon: require('~/assets/sideBar/Settings.png'),
          title: 'Settings and profile',
          hover: false
        },
        {
          id: 6,
          icon: require('~/assets/sideBar/Exams.png'),
          title: 'Exams',
          hover: false
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
      subItem: require('~/assets/sideBar/vector.png'),
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  mounted () {
    this.items.forEach((item) => {
      item.hover = false
      item.visible = false
      item.rotated = false
    })
  },
  methods: {
    handleItem (item) {
      if (!item.to) {
        //
      }
    },
    toggleSubItems (item) {
      item.visible = !item.visible // Cambia el estado de visibilidad
      item.rotated = !item.rotated
    }
  }
}
</script>

<style>

.v-icon {
  display: none;
  transition: transform 0.3s ease-in-out
}

.list-item-hover .v-icon, .list-item-active .v-icon {
  display: block;
}

.list-item, .sub-item {
  width:242px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 4px 12px;
  border-radius: 12px;
}

.item-icon, .sub-item-icon .icon-chevron {
  width: 15px;
  height: 15px;
  object-fit: contain;
}

.icon-sublist {
  vertical-align: middle;
  width: 2px;
  height: 6px;
  object-fit: contain;
}

.item-title {
  font-size: 14px;
  font-weight: 600;
  line-height: 17.36px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 180px; /* Adjust based on your design */
  flex: 1;
}

.sub-item-title{
  font-size: 14px;
  font-weight: 600;
  line-height: 17.36px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 180px; /* Adjust based on your design */
  flex: 1;
  margin-right: 10px;
}

.sub-item-list {
  background-color: #121C4A;
  padding-top: 0;
  margin-top: 0;
}

.sub-item {
  width: 242px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 4px 12px;
  border-radius: 12px; /* Slightly darker for distinction */
}

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

.list-item-hover:hover, .list-item-active {
  background-color: #509CDB;
  color: white;
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
