<template>
  <v-app>
    <v-container class="my-5">
      <v-app-bar app dense :style="{ backgroundColor: 'transparent', marginBottom: '3rem', marginTop:'2rem' }" elevation="0">
        <v-toolbar-title>Company name</v-toolbar-title>
        <v-spacer /> <!-- Este v-spacer empuja todo lo que sigue hacia el centro -->

        <!-- Botones centrados con estilo personalizado -->
        <v-btn text href="#" class="button-style">
          Home
        </v-btn>
        <v-btn text href="#" class="button-style">
          Pricing
        </v-btn>
        <v-btn text href="#" class="button-style">
          Use Cases
        </v-btn>
        <v-btn text href="#" class="button-style">
          Location
        </v-btn>
        <v-btn text href="#" class="button-style">
          FAQ
        </v-btn>
        <v-btn text href="#" class="button-style">
          Company
        </v-btn>

        <v-spacer /> <!-- Este v-spacer empuja todo lo que está antes hacia la izquierda y lo que sigue hacia la derecha -->
        <v-btn outlined color="primary" href="#">
          Sign up
        </v-btn>
      </v-app-bar>

      <!-- Añadiendo un margen superior al v-row para separarlo del v-app-bar -->
      <v-row justify="center" style="margin-top: 3rem;">
        <v-col cols="12" sm="8">
          <div class="text-center">
            <h1 class="display-2">
              Manage your team easily with task man
            </h1>
            <p class="subtitle-1">
              Quickly build an effective pricing table for your potential customers with this Vuetify example. It's built with default Vuetify components and utilities with little customization.
            </p>
          </div>
        </v-col>
      </v-row>

      <v-row>
        <v-col v-for="plan in plans" :key="plan.title" cols="12" md="4">
          <v-card class="mx-auto" outlined>
            <v-card-title>{{ plan.title }}</v-card-title>
            <v-card-subtitle>
              <h1>${{ plan.price }} <span class="grey--text">/ mo</span></h1>
            </v-card-subtitle>
            <v-card-text>
              <v-list>
                <v-list-item v-for="feature in plan.features" :key="feature" dense>
                  <v-list-item-content>{{ feature }}</v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card-text>
            <v-card-actions>
              <v-btn :color="plan.buttonColor" block @click="subscribe(plan.title)">
                {{ plan.buttonText }}
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <v-footer fixed padless>
      <v-col class="text-center" cols="12">
        <v-small>&copy; 2017-2023</v-small>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    plans: [
      {
        title: 'Free',
        price: '0',
        features: ['10 users included', '2 GB of storage', 'Email support', 'Help center access'],
        buttonText: 'Sign up for free',
        buttonColor: 'primary'
      },
      {
        title: 'Pro',
        price: '15',
        features: ['20 users included', '10 GB of storage', 'Priority email support', 'Help center access'],
        buttonText: 'Get started',
        buttonColor: 'primary'
      },
      {
        title: 'Enterprise',
        price: '29',
        features: ['30 users included', '15 GB of storage', 'Phone and email support', 'Help center access'],
        buttonText: 'Contact us',
        buttonColor: 'primary'
      }
    ]
  }),
  methods: {
    subscribe (plan) {
      alert(`Subscribed to ${plan}`)
    }
  }
}
</script>

<style scoped>
.button-style {
  font-family: 'Karla', sans-serif;
  font-size: 12px;
  font-weight: 400;
  line-height: 14.03px;
  text-align: center;
}
</style>
