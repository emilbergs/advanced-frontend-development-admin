<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Produkter</router-link> |
      <router-link to="/create">Nyt produkt</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
  border: 1px solid;
  padding: 5px;
}

#nav a.router-link-exact-active {
  color: lightblue;
}
body{
  background:white;
}

/* Demo Purpose Only*/
.demo {
  font-family: 'Raleway', sans-serif;
	color:#fff;
    display: block;
    margin: 0 auto;
    padding: 15px 0;
    text-align: center;
}
.demo a{
  font-family: 'Raleway', sans-serif;
color: #000;		
}
</style>
