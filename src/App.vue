<template>
  <div id="app">
    <!-- render page -->
    <router-view></router-view>
  </div>
</template>



<style>
/* reset style */
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

li {
  list-style-type: none;
}
a {
  text-decoration: none;
  color: #25485f;
  font-weight: 700;
  font-size: 20px;
}
a:hover {
  color: #00ba81;
}
/* id app */
#app {
  background: linear-gradient(to bottom right, #6ae0ab, #0b224e);
  font-family: "Roboto", sans-serif;
}

/* media adaptiv */
/* @media screen and (max-width: 850px) {
  #app {
    height: 100%;
  }
} */
</style>
