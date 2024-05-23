<template>
  <v-app>
    <!-- Toolbar -->
    <v-app-bar color="#100F57" fixed app elevation="0">
      <!-- Logo Image -->
      <img src="/Statisda.png" alt="Company Logo" class="nav-company-logo">

      <!-- Container for Centered Buttons -->
      <v-spacer /> <!-- Espaciador antes de los botones para centrar -->
      <div class="button-container">
        <!-- Contenedor para los botones -->
        <v-btn text class="button-text-transform btn-spacing" href="#">
          Home
        </v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">
          Pricing
        </v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">
          Use Cases
        </v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">
          Location
        </v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">
          FAQ
        </v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">
          Company
        </v-btn>
      </div>
      <v-spacer /> <!-- Espaciador después de los botones para centrar -->

      <!-- Right Button -->
      <v-btn class="button-text-transform sign-up-btn" @click="redirectLogin">
        Login
      </v-btn>
    </v-app-bar>

    <!-- Main content area -->
    <v-main>
      <!-- Custom Section Below Toolbar -->
      <div class="full-width-section">
        <div class="custom-button-container">
          <v-btn class="custom-consultation-button">
            Get Your Consultation Now
          </v-btn>
        </div>
        <div class="title-text-container">
          <div class="title-text">
            Manage your team
          </div>
          <div class="title-text">
            easily with task man
          </div>
          <div class="sub-title-text1">
            <!-- Nuevo texto añadido aquí -->
            Statisdaa is a school management solution that offers
          </div>
          <div class="sub-title-text2">
            <!-- Nuevo texto añadido aquí -->
            a personalized portal to each type of user.
          </div>
          <v-btn class="button-text-transform get-started-btn" href="#">
            <!-- Aplicamos la nueva clase aquí -->
            Get Started
          </v-btn>

          <!-- Nueva imagen agregada aquí -->
          <img src="~/assets/Fotoq.png" alt="Descripción de la imagen" class="image-below-button">
        </div>
      </div>

      <div class="trusted-by">
        Trusted by company like
      </div>

      <v-container>
        <v-row justify="center" class="logo-row">
          <v-col cols="auto" class="logo-col">
            <v-img src="/logo3.png" alt="Logo 1" class="company-logo" />
          </v-col>
          <v-col cols="auto" class="logo-col">
            <v-img src="/logo2.png" alt="Logo 2" class="company-logo" />
          </v-col>
          <v-col cols="auto" class="logo-col">
            <v-img src="/logo1.png" alt="Logo 3" class="company-logo" />
          </v-col>
          <v-col cols="auto" class="logo-col">
            <v-img src="/logo3.png" alt="Logo 1" class="company-logo" />
          </v-col>
          <v-col cols="auto" class="logo-col">
            <v-img src="/logo2.png" alt="Logo 2" class="company-logo" />
          </v-col>
          <v-col cols="auto" class="logo-col">
            <v-img src="/logo1.png" alt="Logo 3" class="company-logo" />
          </v-col>
        </v-row>
      </v-container>

      <v-container class="my-separator" />

      <v-container>
        <v-row>
          <!-- Slack Integration Cards Column -->
          <v-col cols="12" md="8">
            <v-row>
              <v-col v-for="n in 4" :key="n" cols="12" md="6">
                <v-card class="slack-card" elevation="2">
                  <v-card-title class="headline font-weight-bold">
                    Slack integration
                  </v-card-title>
                  <v-card-subtitle class="subtile-slack">
                    Statisdaa is a school management solution that offers a personalized portal to each type of user.
                  </v-card-subtitle>
                  <v-card-text>
                    <div class="d-flex align-center">
                      <!-- Development button and Avatar group -->
                      <v-btn class="development-btn ma-2 text-capitalize" elevation="0">
                        Development
                      </v-btn>
                      <v-avatar-group>
                        <v-avatar size="24" class="ma-1">
                          <img src="https://cdn.vuetifyjs.com/images/lists/1.jpg">
                        </v-avatar>
                        <v-avatar size="24" class="ma-1">
                          <img src="https://cdn.vuetifyjs.com/images/lists/2.jpg">
                        </v-avatar>
                        <v-avatar size="24" class="ma-1">
                          <img src="https://cdn.vuetifyjs.com/images/lists/3.jpg">
                        </v-avatar>
                      </v-avatar-group>
                    </div>
                    <v-divider class="my-3" />
                    <div class="d-flex justify-space-between align-center">
                      <v-chip class="custom-chip">
                        14
                      </v-chip>
                      <div>
                        <v-icon class="mr-1">
                          mdi-calendar
                        </v-icon>
                        <span>7 feb 2022</span>
                      </div>
                    </div>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-col>

          <!-- Create Your Task Column -->
          <v-col cols="12" md="4">
            <v-card class="mx-auto my-2" elevation="2" max-width="100%">
              <v-card-title class="task-title">
                Create your task
              </v-card-title>
              <v-card-subtitle class="task-subtitle">
                Statisdaa is a school management solution that offers a personalized portal to each type of user, ensuring that your institution is always engaged with teachers, students, and their parents.
              </v-card-subtitle>
              <v-card-text>
                <v-form>
                  <v-text-field
                    label="Create your task"
                    outlined
                    dense
                    placeholder="Create your task"
                  />
                  <v-text-field
                    label="Create your task"
                    outlined
                    dense
                    placeholder="Create your task"
                  />
                  <!-- Blue Box with Vuetify components -->
                  <v-card color="#0A92DD" dark class="mt-4">
                    <v-card-title class="info-title">
                      Manage the task easily and clearly
                    </v-card-title>
                    <v-card-subtitle class="create-manage">
                      Statisdaa increases communication between all stakeholders: students, teachers, parents, and administrative staff, with a dedicated web portal for any type of end-user. Keeping your students and parents engaged with the academic process is a crucial factor in each student's success.
                    </v-card-subtitle>
                  </v-card>
                </v-form>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <v-container class="my-separator" />
      <v-container class="my-separator" />

      <v-container>
        <v-row>
          <!-- Column for Text -->
          <v-col cols="12" md="6">
            <div class="formatted-text">
              <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet ut lobortis pellentesque a, luctus maecenas.</p>
              <p>Feugiat sed enim vitae viverra cras tristique eu. Pellentesque bibendum volutpat metus, dictum.</p>
              <!-- Fila para el ícono y el texto -->
              <v-row align="center" no-gutters>
                <v-col cols="auto">
                  <v-avatar size="80">
                    <!-- Tamaño del contenedor del ícono -->
                    <v-icon size="60">
                      mdi-account-circle
                    </v-icon> <!-- Tamaño específico del ícono -->
                  </v-avatar>
                </v-col>
                <v-col>
                  <div class="display-1">
                    80,000K
                  </div>
                  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
                </v-col>
              </v-row>
            </div>
          </v-col>
          <v-col cols="12" md="6">
            <v-card flat>
              <v-img
                src="/mano.png"
                alt="A descriptive alt text"
                class="move-image-up elevation-0"
              />
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <v-container>
        <v-row>
          <v-col>
            <h1 class="plan-title">
              Pick up the best plan
            </h1>
            <!-- Contenedor para el texto dividido en tres líneas -->
            <div class="multi-line-text">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet ut lobortis pellentesque a, luctus maecenas.
            </div>
          </v-col>
        </v-row>

        <v-container class="my-separator" />

        <v-row justify="center">
          <!-- Primera Tarjeta -->
          <v-col cols="12" md="4">
            <v-card class="custom-card" elevation="6">
              <v-card-title class="custom-card-title">
                Standard
              </v-card-title>
              <v-card-text class="custom-card-text">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet
              </v-card-text>
              <v-card-subtitle class="custom-card-subtitle">
                <span class="price-big">$15</span> /Month
              </v-card-subtitle>
              <v-divider /> <!-- Divisor -->
              <v-list dense class="custom-card-list">
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
              </v-list>
              <v-card-actions class="custom-card-actions justify-center">
                <v-btn class="custom-button">
                  Choose
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
          <!-- Segunda Tarjeta -->
          <v-col cols="12" md="4">
            <v-card class="custom-card-second" dark>
              <v-card-title class="custom-card-title-second">
                Standard
              </v-card-title>
              <v-card-text class="custom-card-text">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet
              </v-card-text>
              <v-card-subtitle class="custom-card-subtitle">
                <span class="price-big">$15</span> /Month
              </v-card-subtitle>
              <v-divider />
              <v-list dense class="custom-card-list-second">
                <v-list-item class="custom-bg-color">
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
                <v-list-item class="custom-bg-color">
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
                <v-list-item class="custom-bg-color">
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
              </v-list>
              <v-card-actions class="custom-card-actions-second justify-center">
                <v-btn class="custom-button-second">
                  Choose
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
          <!-- Tercera Tarjeta -->
          <v-col cols="12" md="4">
            <v-card class="custom-card" elevation="6">
              <v-card-title class="custom-card-title">
                Standard
              </v-card-title>
              <v-card-text class="custom-card-text">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet
              </v-card-text>
              <v-card-subtitle class="custom-card-subtitle">
                <span class="price-big">$15</span> /Month
              </v-card-subtitle>
              <v-divider /> <!-- Divisor -->
              <v-list dense class="custom-card-list">
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-checkbox-blank-circle</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    For 1-10 people in a team
                  </v-list-item-content>
                </v-list-item>
              </v-list>
              <v-card-actions class="custom-card-actions justify-center">
                <v-btn class="custom-button">
                  Choose
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <v-container class="my-separator" />

      <v-container>
        <!-- Nueva Sección con Título y Descripción -->
        <v-row>
          <v-col cols="12" md="6">
            <!-- Columna para el Título -->
            <h2 class="custom-title">
              Interesting option from customer
            </h2>
          </v-col>
          <v-col cols="12" md="6">
            <!-- Columna para el Texto Descriptivo -->
            <div class="text-container">
              <p class="custom-description">
                <span>Lorem ipsum dolor sit amet, consectetur </span>
                <span>adipiscing elit. Purus odio pellentesque </span>
                <span>pellentesque a. Amet</span>
              </p>
            </div>
          </v-col>
        </v-row>
      </v-container>

      <v-container>
        <v-row class="big-container" align="center" justify="center">
          <!-- Imagen a la derecha -->
          <v-col cols="12" md="6" class="px-md-12">
            <v-img
              src="/customer.png"
              alt="Customer Image"
              class="big-image"
            />
          </v-col>
          <!-- Tarjeta a la izquierda -->
          <v-col cols="12" md="4">
            <v-card class="custom-card-left" dark>
              <v-card-title class="custom-card-title-left">
                Standard
              </v-card-title>
              <v-card-text class="custom-card-text-left">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet
              </v-card-text>
              <v-card-subtitle class="custom-card-subtitle-left">
                <span class="price-big-left">$15</span> /Month
              </v-card-subtitle>
              <v-card-actions class="custom-card-actions-left justify-center">
                <v-btn class="custom-button-left">
                  Choose
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <v-container>
        <!-- Fila del contenedor principal para la sección -->
        <v-row>
          <!-- Columna para la imagen del teclado -->
          <v-col cols="12" md="6">
            <v-img
              src="/teclado.png"
              alt="Customer Image"
              class="big-image"
            />
          </v-col>
          <!-- Columna para el contenido textual -->
          <v-col cols="12" md="6">
            <div>
              <h2 class="section-title">
                Interesting option from customer
              </h2>
              <p class="section-text">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Eget id arcu mauris sed augue volutpat tortor. Condimentum facilisis anean elit sed mattis porttitor duis ornare justo.
              </p>
              <v-btn class="btn-teclado">
                Choose
              </v-btn>
            </div>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <!-- Footer -->
    <v-footer color="#100F57" class="pa-10">
      <v-container fluid>
        <v-row>
          <!-- Columnas de Enlaces -->
          <v-col cols="12" sm="3" class="footer-col">
            <h3 class="footer-heading">
              Lorem ipsum dolor
            </h3>
            <p class="white-text">
              Home jjjjjjjjj
            </p>
            <p class="white-text">
              Pricing hfdhdfj
            </p>
            <p class="white-text">
              Use cases jsksi
            </p>
            <p class="white-text">
              Location hdhdhd
            </p>
            <p class="white-text">
              FAQ kdkdkdd
            </p>
            <p class="white-text">
              Company jdksodk
            </p>
          </v-col>
          <!-- Repetir la estructura anterior para las siguientes dos columnas -->
          <v-col cols="12" sm="3" class="footer-col">
            <h3 class="footer-heading">
              Lorem ipsum dolor
            </h3>
            <p class="white-text">
              Home jjjjjjjjj
            </p>
            <p class="white-text">
              Pricing hfdhdfj
            </p>
            <p class="white-text">
              Use cases jsksi
            </p>
            <p class="white-text">
              Location hdhdhd
            </p>
            <p class="white-text">
              FAQ kdkdkdd
            </p>
            <p class="white-text">
              Company jdksodk
            </p>
          </v-col>
          <v-col cols="12" sm="3" class="footer-col">
            <h3 class="footer-heading">
              Lorem ipsum dolor
            </h3>
            <p class="white-text">
              Home jjjjjjjjj
            </p>
            <p class="white-text">
              Pricing hfdhdfj
            </p>
            <p class="white-text">
              Use cases jsksi
            </p>
            <p class="white-text">
              Location hdhdhd
            </p>
            <p class="white-text">
              FAQ kdkdkdd
            </p>
            <p class="white-text">
              Company jdksodk
            </p>
          </v-col>
          <!-- Columna para el botón de consulta -->
          <v-col cols="12" sm="3" class="footer-col">
            <h3 class="footer-heading">
              Lorem ipsum dolor
            </h3>
            <p class="white-text">
              Home jjjjjjjjj
            </p>
            <div class="consultation-container">
              <span class="consultation-text">Get Your Free Consultation Now</span>
              <v-btn class="btn-consultation ml-2" color="primary">
                Get Started
              </v-btn>
            </div>
          </v-col>
        </v-row>
        <!-- Fila para el texto de derechos de autor y enlaces legales alineados a la derecha -->
        <v-container class="my-separator" />
        <v-row>
          <v-col cols="12" sm="6" class="white--text text-left">
            ©2024 Scholl Management. Copyright And All Rights Reserved.
          </v-col>
          <v-col cols="12" sm="6" class="white--text d-flex justify-end legal-links">
            <span class="mr-3">Privacy</span>
            <span class="mr-3">Security</span>
            <span>Terms</span>
          </v-col>
        </v-row>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  methods: {
    redirectLogin () {
      this.$router.push('/login')
    }
  }
}
</script>

<style>
.consultation-container {
  display: flex;
  align-items: center;
  padding: 8px;
  background-color: #FFFFFF;
  border-radius: 9px 9px 9px 9px;
}

.consultation-text {
  font-family: 'Karla', sans-serif; /* Especifica la fuente Karla */
  font-size: 14px; /* Tamaño de la fuente a 14px */
  font-weight: 500; /* Peso de la fuente a medio */
  line-height: 16.37px; /* Altura de línea */
  text-align: center; /* Alineación del texto al centro */
  color: #667085 !important; /* Color del texto a gris oscuro */
  margin-right: 10px; /* Espacio entre el texto y el botón */
}

.btn-consultation {
  width: 129px; /* Ancho fijo */
  height: 48px; /* Altura fija */
  padding: 10px 14px; /* Ajuste del relleno */
  border-radius: 40px 40px 40px 40px; /* Bordes redondeados */
  border: 0.2px solid transparent; /* Borde transparente, ajusta si necesitas color */
  opacity: 1; /* Ajusta la opacidad (nota que 0px no mostrará el botón) */
  text-transform: none;
}

.v-app-bar .v-btn {
  color: white !important;
  font-family: 'Karla', sans-serif;
  font-size: 12px;
  font-weight: 400;
  line-height: 14.03px;
  text-align: center;
  margin-right: 10px; /* Adjust spacing between buttons */
}

/* Responsiveness */
@media (max-width: 600px) {
  .v-app-bar {
    flex-direction: column;
    align-items: center;
  }
  .button-container {
    flex-direction: column;
    align-items: center;
  }
}

/* Estilos específicos para el logo */
.company-logo {
  width: 98px;
  height: 26px;
  opacity: 1; /* Asegúrate que la imagen es visible */
  margin-left: 20px;
  margin-right: 20px;
}
.nav-company-logo {
  width: 98px;
  height: 26px;
  opacity: 1; /* Asegúrate que la imagen es visible */
  margin-left: 20px;
  margin-right: 20px;
}

.button-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap; /* Permite que los botones se ajusten en múltiples líneas si es necesario */
}

/* Clase para aplicar margen a los botones */
.btn-spacing {
  margin-right: 20px; /* Ajusta este valor según sea necesario para separar los botones */
}

.get-started-btn {
  font-family: 'Karla', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 18.7px;
  text-align: center;
  color: white !important; /* Texto blanco */
  background-color: #0A92DD !important; /* Color de fondo azul */
  border-radius: 40px; /* Bordes redondeados */
  padding: 10px 14px; /* Espaciado interno */
  text-transform: capitalize; /* Texto con mayúscula inicial */
  margin-top: 20px; /* Espacio adicional encima del botón si es necesario */
}

/* Estilos específicos para el botón Login */
.sign-up-btn {
  width: 90px;
  height: 34px;
  padding: 10px 14px 10px 14px;
  background-color: #0A92DD !important;
  border-radius: 40px 40px 40px 40px;
  color: white;
}

/* New custom button styles */
.custom-button-container {
  display: flex;
  justify-content: center;
  margin-top: 20px; /* Space below the toolbar */
}

.custom-consultation-button {
  font-family: 'Karla', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 18.7px;
  text-align: center;
  color: #D89925 !important; /* Texto blanco */
  background-color:  rgb(28, 27, 96) !important; /* Color de fondo azul */
  border-radius: 40px; /* Bordes redondeados */
  padding: 10px 14px; /* Espaciado interno */
  text-transform: capitalize; /* Texto con mayúscula inicial */
}
.title-text-container {
  text-align: center; /* Centering the text */
  margin-top: 20px; /* Space below the button */
}

.title-text {
  font-family: 'Karla', sans-serif; /* Setting the font family */
  font-size: 48px;
  font-weight: 700;
  line-height: 59.53px;
  color: #FFFFFF; /* White text color */
}

.full-width-section {
  width: 100%;
  background: linear-gradient(to bottom, #100F57 63%, white 50%); /* Gradiente ajustado */
  padding: 20px 0; /* Padding for aesthetic */
}

.sub-title-text1 {
  font-family: 'Karla', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 18.7px;
  text-align: center;
  color: #FFFFFF; /* Color de texto blanco */
  margin-top: 20px;
}
.sub-title-text2 {
  font-family: 'Karla', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 18.7px;
  text-align: center;
  color: #FFFFFF; /* Color de texto blanco */
}

.image-below-button {
  width: 931px; /* Ancho fijo de 931px */
  height: 672px; /* Alto fijo de 672px */
  display: block; /* Asegura que la imagen sea un bloque para aplicar márgenes */
  margin: 20px auto; /* Margen superior e inferior de 20px, centrado horizontalmente */
  border-radius: 10px; /* Curvatura de 10px en las esquinas */
}

.trusted-by {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 36px;
  font-weight: 600;
  line-height: 44.65px;
  text-align: center;
  color: #000000; /* Ajusta según el color de fondo */
  margin-top: 20px;
  position: relative;
  z-index: 2; /* Asegura que esté sobre cualquier fondo o imagen */
}

/* Estilos para los logos */
.company-logo {
  width: 44px; /* Ancho especificado */
  height: 46px; /* Altura especificada */
}

/* Estilos adicionales para la fila y columna que contiene los logos */
.logo-row {
  margin-top: 20px; /* Añadir un margen superior si es necesario */
}

.logo-col {
  display: flex;
  justify-content: center; /* Centra los logos horizontalmente */
  align-items: center; /* Centra los logos verticalmente */
  padding: 25px; /* Añadir algo de padding para espaciar los logos */
}

.slack-card {
    width: 350px; /* Adjusted width to fit elements on one line */
    height: auto; /* Adjusted height for content fit */
    opacity: 1;
  }

  .development-btn {
    background:#FFF9EB !important;  /* Background color */
    color: #D89925 !important; /* Font color */
    font-family: 'Kumbh Sans', sans-serif; /* Font family */
    font-size: 12px; /* Font size */
    font-weight: 500; /* Font weight */
    line-height: 14.88px; /* Line height */
    text-align: left; /* Text alignment */
    border-radius: 25px; /* Rounded corners */
    margin-right: 10px; /* Added margin for spacing */
  }

  .v-avatar-group {
    margin-left: 0; /* Adjusted to align better with the button */
  }

  .v-avatar {
    margin-right: -8px; /* Overlapping avatars slightly */
  }

  .my-separator {
    margin-top: 50px; /* Adjust the margin as needed for visual separation */
  }

  .custom-chip {
    background-color: #FFFFFF !important; /* Background color set to white */
    color: #000000; /* Text color set to black */
  }

  .subtile-slack {
    color: #bdbdbd !important;
  }

  .task-title {
    font-family: 'Kumbh Sans', sans-serif;
    font-size: 32px;
    font-weight: 600;
    line-height: 39.69px;
    text-align: left;
    color: #333;
    margin-bottom: 25px; /* Add space between title and subtitle */
  }

  .task-subtitle {
    font-family: 'Kumbh Sans', sans-serif;
    font-size: 14px;
    font-weight: 400;
    line-height: 17.36px;
    text-align: left;
    color: #bdbdbd !important;
    margin-top: 16px; /* Optionally adjust if more space is needed */
  }

  .v-text-field__slot, .v-textarea__slot {
    font-family: 'Kumbh Sans', sans-serif;
  }

  .info-box {
    background-color: #1777f7 !important; /* Adjust the color to match the blue from the image */
    color: white;
    padding: 10px;
    border-radius: 5px;
    margin-top: 20px; /* Space above the blue box */
  }

  .v-text-field__slot {
    font-family: 'Kumbh Sans', sans-serif;
  }

  .info-title {
    font-family: 'Kumbh Sans', sans-serif;
    font-size: 16px; /* Adjusted for visual hierarchy */
    font-weight: 600;
    margin-bottom: 20px;
  }

  .formatted-text h2 {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 24px;
  font-weight: bold;
  line-height: 1.3;
  margin-bottom: 16px;
  text-align: left; /* Ensure the title is left-aligned */
}

.formatted-text p {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 16px;
  line-height: 1.6;
  text-align: left; /* Ensure paragraphs are left-aligned */
  margin-bottom: 12px;
  text-indent: 0px; /* Remove any indent */
  color: #667085 !important;
}

.move-image-up {
  transform: translate(150px, -65px); /* Ajusta este valor según la necesidad */

}

.formatted-text h2, .formatted-text p, .display-1 {
  /* Tus estilos existentes */
  text-align: left;
}

.display-1 {
  font-size: 3rem;
  font-weight: bold;
}

.formatted-text h2, .formatted-text p {
  text-align: left;
}

.create-manage {
  font-size: 10px;
}

.plan-title {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 40px;
  font-weight: 600;
  line-height: 49.61px;
  text-align: center;
  color: #1777F7; /* Azul personalizado */
}

.multi-line-text {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 20px;
  font-weight: 400;
  line-height: 31.59px;
  text-align: center;
  color: #667085; /* Gris personalizado */
  width: 60%; /* Controla el ancho para forzar el texto a dividirse en tres líneas */
  max-width: 700px; /* Ajusta según el tamaño máximo deseado */
  margin: 0 auto; /* Centra el texto horizontalmente */
}

.custom-bg-color {
  background-color: #0B0641 !important; /* Asegura que el color se aplique con !important */
}

.custom-card, .custom-card-second {
  width: 360px;
  height: 524px;
  position: relative;
  border-radius: 8px 0px 0px 0px;
  padding: 16px;
}

.custom-card-second {
  top: -35px;
  background-color: #0B0641 !important; /* Color de fondo específico para la segunda tarjeta */
}

.custom-card-title, .custom-card-text, .custom-card-subtitle, .custom-card-actions, .custom-card-list {
  padding: 0 12px;
  margin-bottom: 12px; /* Espacio añadido entre componentes */
}

.custom-card-title {
  color: #1777F7;
  padding: 4px 8px;
  margin-top: 10px;
}

.custom-card-title-second {
  color: #1777F7;
  margin-top: 5px;
}

.custom-card-text {
  margin-bottom: 50px; /* Espacio añadido entre componentes */
}

.custom-card-list {
  padding-left: 12px; /* Padding sólo para la lista dentro de la tarjeta */
  margin-top: 20px; /* Espacio añadido entre componentes */
}

.custom-card-list-second {
  padding-left: 12px; /* Padding sólo para la lista dentro de la tarjeta */
  background-color: #0B0641 !important;
  margin-top: 20px;
}

.custom-card-actions {
  margin-top: 40px;
}

.custom-card-actions-second {
  margin-top: 20px;
}

.price-big {
  font-size: 32px; /* Tamaño de fuente aumentado para el número $15 */
  font-weight: bold; /* Hacer el número más destacado */
}

.custom-button {
  width: 279px; /* Ancho fijo */
  height: 33px; /* Altura fija */
  padding: 8px 20px; /* Padding especificado */
  border-radius: 9px 9px 9px 9px; /* Radio de borde */
  position: absolute; /* Posicionamiento absoluto */
  background: #1777F7 !important;
  color: #FFFFFF !important;
  margin-top: 60px;
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 14px;
  font-weight: 500;
  line-height: 17.36px;
  text-align: left;
  text-transform: none; /* Elimina la transformación a mayúsculas */
}

.custom-button-second {
  width: 279px; /* Ancho fijo */
  height: 33px; /* Altura fija */
  padding: 8px 20px; /* Padding especificado */
  border-radius: 9px 9px 9px 9px; /* Radio de borde */
  position: absolute; /* Posicionamiento absoluto */
  background: #1777F7 !important;
  color: #FFFFFF !important;
  margin-top: 50px;
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 14px;
  font-weight: 500;
  line-height: 17.36px;
  text-align: left;
  text-transform: none; /* Elimina la transformación a mayúsculas */
}

.custom-title {
  font-family: 'Kumbh Sans', sans-serif; /* Fuente Kumbh Sans */
  font-size: 40px; /* Tamaño de fuente */
  font-weight: 600; /* Peso de la fuente */
  line-height: 49.61px; /* Altura de línea */
  text-align: left; /* Alineación del texto a la izquierda */
  color: #1E2024 !important; /* Color de texto */
}

.text-container {
  max-width: 550px; /* Puedes ajustar este valor según sea necesario */
}

.custom-description {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 20px;
  font-weight: 400;
  line-height: 31.59px;
  text-align: left;
  color: #667085 !important;
  display: block; /* Asegura que el párrafo se maneje como un bloque */
}

.custom-description span {
  display: block; /* Hace que cada span ocupe su propia línea */
}

.big-image {
  max-width: 100%; /* Asegura que la imagen no exceda el tamaño del contenedor */
  height: auto; /* Mantiene la proporción de la imagen */
}

.big-container {
  margin-top: 20px; /* Espacio adicional desde la sección anterior */
  background-color: #0B0641; /* Fondo del contenedor grande */
  padding: 80px; /* Padding interno para la estética */
  border-radius: 9px 9px 9px 9px;
}

.custom-card-left {
  top: -35px;
  background-color: #0B0641 !important;
  position: relative;
  border-radius: 8px 0px 0px 0px;
  padding: 16px;
}
.custom-card-title-left {
  color: #1777F7;
  margin-top: -50px;
}

.custom-card-text-left {
  margin-bottom: 50px; /* Espacio añadido entre componentes */
}

.price-big-left {
  font-size: 32px; /* Tamaño de fuente aumentado para el número $15 */
  font-weight: bold; /* Hacer el número más destacado */
}

.custom-card-actions-left {
  margin-top: 20px;
}

.custom-card-title-left, .custom-card-text-left, .custom-card-subtitle-left, .custom-card-actions-left, .custom-card-list {
  padding: 0 12px;
  margin-bottom: 12px; /* Espacio añadido entre componentes */
}

.custom-card-subtitle-left {
  margin-top: 40px;
}

.custom-button-left {
  width: 279px; /* Ancho fijo */
  height: 33px; /* Altura fija */
  padding: 8px 20px; /* Padding especificado */
  border-radius: 9px 9px 9px 9px; /* Radio de borde */
  position: absolute; /* Posicionamiento absoluto */
  background: #1777F7 !important;
  color: #FFFFFF !important;
  margin-top: 222px;
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 14px;
  font-weight: 500;
  line-height: 17.36px;
  text-align: left;
  text-transform: none; /* Elimina la transformación a mayúsculas */
}

.section-title {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 40px;
  font-weight: 600;
  line-height: 49.61px;
  text-align: left;
  color: #1E2024;
  margin-bottom: 20px;
  margin-top: 100px;
}

.section-text {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 31.59px;
  text-align: left;
  color: #667085;
  margin-bottom: 20px;
}
.btn-teclado {
  width: 139px; /* Ancho fijo */
  height: 33px; /* Altura fija */
  padding: 8px 20px; /* Padding especificado */
  border-radius: 9px 9px 9px 9px; /* Radio de borde */
  position: absolute; /* Posicionamiento absoluto */
  background: #1777F7 !important;
  color: #FFFFFF !important;
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 14px;
  font-weight: 500;
  line-height: 17.36px;
  text-align: left;
  text-transform: none; /* Elimina la transformación a mayúsculas */
  margin-top: 20px;
}

.footer-heading {
  color: #FFFFFF;
  font-weight: bold;
  margin-bottom: 12px;
  font-family: 'Karla', sans-serif;
}
.footer-col {
  text-align: left; /* Alinea el texto a la izquierda en las columnas */
}

.white-text {
  color: #FFFFFF; /* Establece el color de texto a blanco */
  font-size: 12px;
  font-family: 'Karla', sans-serif;
}

.legal-links {
  padding-right: 150px; /* Añade 30px de padding derecho para mover los enlaces a la izquierda */
}

</style>
