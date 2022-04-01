<template>
  <nav class="menu-telas">
    <div class="container">
      <div class="row">
        <div class="col-4 col-md-2 offset-md-3">
          <router-link to="/" class="d-flex align-items-center flex-column item-menu-telas">
            <img src="@/assets/checkout.svg" alt="" class="img-fluid mx-auto">
            <span>Checkout</span>
          </router-link> 
        </div>
        <div class="col-4 col-md-2">            
          <router-link to="/cozinha" class="d-flex align-items-center flex-column item-menu-telas">
            <img src="@/assets/cozinha.svg" alt="" class="img-fluid mx-auto">
            <span>Cozinha</span>
          </router-link>
        </div>
        <div class="col-4 col-md-2">            
            <router-link to="/retirar" class="d-flex align-items-center flex-column item-menu-telas">
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

@import './scss/style.scss';

#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--dark);
  background-color: var(--light);
}

nav.menu-telas {
  padding: 110px 0 30px;
  background-color: var(--light);
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
  border: 1px solid var(--neutral);
  border-radius: 10px;
  padding: 10px 0;
  background-color: var(--white);
}

 h2 {
  // text-transform: uppercase;
  font-weight: 700;
  text-align: left;
  font-size: 16px;  
} 

</style>
