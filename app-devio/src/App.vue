<template>
  <nav class="menu-telas">
    <div class="container">
      <div class="row">
        <div class="col-4 col-md-2 offset-md-3 item-menu-telas">
              <router-link to="/">Checkout</router-link> 
        </div>
        <div class="col-4 col-md-2 item-menu-telas">
              <router-link to="/cozinha">Cozinha</router-link> 
        </div>
        <div class="col-4 col-md-2 item-menu-telas">
              <router-link to="/retirar">Retirar</router-link>
        </div>
      </div>
    </div>
  </nav>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333333;
  background-color: #f4f4f4;
}

nav.menu-telas {
  padding: 80px 0 30px;
}

nav.menu-telas a {
  font-weight: bold;
  color: #2c3e50;
  text-transform: uppercase;
  
  text-decoration: none;
}

/* nav.menu-telas a.router-link-exact-active {
  color: #42b983;
} */

div.item-menu-telas {
  border: 1px solid #666;
}
/* h2 {
  text-transform: uppercase;
} */

</style>
