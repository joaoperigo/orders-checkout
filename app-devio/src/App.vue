<template>
  <nav class="menu-telas">
    <div class="container">
      <div class="row">
        <div class="col-4 col-md-2 offset-md-3">
          <router-link to="/" class="d-flex align-items-center flex-column bg-primary item-menu-telas">
            <img src="@/assets/checkout.svg" alt="" class="img-fluid mx-auto">
            <span>Checkout</span>
          </router-link> 
        </div>
        <div class="col-4 col-md-2">            
          <router-link to="/cozinha" class="d-flex align-items-center flex-column bg-primary item-menu-telas">
            <img src="@/assets/cozinha.svg" alt="" class="img-fluid mx-auto">
            <span>Cozinha</span>
          </router-link>
        </div>
        <div class="col-4 col-md-2">            
            <router-link to="/retirar" class="d-flex align-items-center flex-column bg-primary item-menu-telas">
              <img src="@/assets/retirada.svg" alt="" class="img-fluid mx-auto">
              <span>Retirar</span>
            </router-link>
        </div>
      </div>
    </div>
  </nav>
  <router-view/>
</template>

<style lang="scss">
:root {
  --primary: #b10438;
  --secondary: #48ff00;
  --tertiary: #ffee01;
  --neutral: #999;
  --neutralDark: #666; 
  --dark: #333;
  --light: #f4f4f4;
  --white: #ffffff;
}
.bg-primary {
  background-color: var(--primary);
}
.bg-secondary {
  background-color: var(--secondary);
}
.bg-tertiary {
  background-color: var(--tertiary);
}

#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--dark);
  background-color: var(--light);
}

nav.menu-telas {
  padding: 100px 0 30px;
}

nav.menu-telas a {
  font-weight: bold;
  color: var(--dark);
  text-transform: uppercase;
  font-size: 14px;
  text-decoration: none;
}

/* nav.menu-telas a.router-link-exact-active {
  color: #42b983;
} */

.item-menu-telas {
  border: 1px dashed var(--neutral);
  border-radius: 10px;
  padding: 10px 0;
  // background-color: var(--white);
}

 h2 {
  // text-transform: uppercase;
  font-weight: 700;
  text-align: center;
  font-size: 16px;  
} 

</style>
