<template>
  <v-app>
    <!-- Toolbar -->
    <v-app-bar color="#100F57" fixed app elevation="0">
      <!-- Logo Image -->
      <img src="/Statisda.png" alt="Company Logo" class="company-logo">

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
      <v-btn class="button-text-transform sign-up-btn" href="#">
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
                  <v-card-subtitle>
                    Statisdaa is a school management solution that offers a personalized portal to each type of user.
                  </v-card-subtitle>
                  <v-card-text>
                    <div class="d-flex align-center">
                      <!-- Development button -->
                      <v-btn class="development-btn ma-2 text-capitalize" elevation="0">
                        Development
                      </v-btn>
                      <!-- Avatar group -->
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
                    <div class="d-flex align-center">
                      <v-icon class="mr-1">
                        mdi-calendar
                      </v-icon>
                      <span>7 feb 2022</span>
                      <v-chip class="ml-auto amber darken-1 white--text">
                        14
                      </v-chip>
                    </div>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-col>

          <!-- Create Your Task Column -->
          <v-col cols="12" md="4">
            <v-card class="mx-auto my-2" elevation="2" max-width="100%">
              <v-card-title>Create your task</v-card-title>
              <v-card-subtitle>Statisdaa is a school management solution that offers a personalized portal to each type of user, ensuring that your institution is always engaged with teachers, students, and their parents.</v-card-subtitle>
              <v-card-text>
                <v-text-field label="Create your task" outlined dense />
                <v-text-field label="Manage the task easily and clearly" outlined dense multiline />
                <v-btn color="primary">
                  Submit
                </v-btn>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <!-- Additional content -->
      <v-container>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <!-- Your repeated content goes here -->
      </v-container>
    </v-main>

    <!-- Footer -->
    <v-footer>
      <v-col class="text-center">
        © 2023 Company Name
      </v-col>
    </v-footer>
  </v-app>
</template>

<style>
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
    background: #D89925; /* Background color */
    color: #FFF9EB; /* Font color */
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
</style>
