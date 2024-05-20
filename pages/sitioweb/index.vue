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

        <!-- Sección de confianza de empresas -->
        <div class="trusted-section">
          <v-container>
            <v-row justify="center">
              <v-col cols="12" class="text-center">
                <span class="trusted-title">Trusted by company like</span>
              </v-col>
              <v-col v-for="n in 5" :key="n" cols="2" md="1">
                <v-img src="~/assets/logo{n}.png" alt="Company Logo" />
              </v-col>
            </v-row>
          </v-container>
        </div>
      </div>

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
@media (max-width: 950px) {
  .v-app-bar {
    flex-direction: column;
    align-items: center;
  }
  .button-container {
    flex-direction: column;
    align-items: center;
  }
  .image-below-button {
    width: 100%; /* Se ajusta al 100% del ancho del contenedor */
    height: auto; /* La altura se ajusta automáticamente para mantener la proporción */
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

.trusted-section {
  margin-top: 40px; /* Espacio sobre la sección para separarla de la imagen */
}

.trusted-title {
  font-size: 24px; /* Tamaño del texto */
  color: #666; /* Color del texto */
  margin-bottom: 20px; /* Espacio debajo del título */
}

.v-col {
  display: flex;
  justify-content: center; /* Centra los logos dentro de las columnas */
  align-items: center; /* Alinea verticalmente los logos */
}

.v-img {
  max-width: 100%; /* Asegura que el logo no sea más grande que su contenedor */
  height: auto; /* Mantiene la proporción del logo */
}

</style>
