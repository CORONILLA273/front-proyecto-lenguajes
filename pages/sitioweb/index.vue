<template>
  <v-app>
    <!-- Toolbar -->
    <v-app-bar color="#100F57" class="d-flex justify-space-between align-center">
      <!-- Logo Image -->
      <img src="/Statisda.png" alt="Company Logo" class="company-logo">

      <!-- Container for Centered Buttons -->
      <div class="button-container">
        <v-btn text class="button-text-transform btn-spacing" href="#">Home</v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">Pricing</v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">Use Cases</v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">Location</v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">FAQ</v-btn>
        <v-btn text class="button-text-transform btn-spacing" href="#">Company</v-btn>
      </div>

      <!-- Right Button -->
      <v-btn class="button-text-transform sign-up-btn" href="#">Login</v-btn>
    </v-app-bar>

    <!-- Main content area -->
    <v-main>
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
        <h1>Welcome to Our Website</h1>
        <p>This is the home page of your site located under /sitioweb.</p>
        <!-- Additional repeated content omitted for brevity -->
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
}

/* Aplica estilos directamente en este componente */
.v-btn .v-btn__content {
  text-transform: capitalize !important; /* Solo capitaliza la primera letra de cada palabra */
}

/* Estilos específicos para el logo */
.company-logo {
  width: 98px;
  height: 26px;
  opacity: 1; /* Asegúrate que la imagen es visible */
  margin-left: 150px;
  margin-right: 400px;
}

.button-container {
  display: flex;
  justify-content: center;
  flex-grow: 1;
}

/* Clase para aplicar margen a los botones */
.btn-spacing {
  margin-right: 20px; /* Ajusta este valor según sea necesario para separar los botones */
}

/* Estilos específicos para el botón Sign up */
.sign-up-btn {
  width:  90px;
  height: 34px;
  padding: 10px 14px 10px 14px;
  background-color: #0A92DD !important;
  border-radius: 40px 40px 40px 40px;
  color: white;
  margin-left: 350px; /* Ajusta según sea necesario para mover el botón a la derecha */
}
</style>
