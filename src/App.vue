<template>
  <div id="app">
    <nav class="navbar navbar-expand" style="background-color: #032f3c">
      <div class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link to="/contacts" class="nav-link text-white"
            >Contacts</router-link
          >
        </li>
        <li class="nav-item">
          <router-link to="/add" class="nav-link text-white"
            >Add contact</router-link
          >
        </li>
      </div>
    </nav>

    <div class="container mt-3">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
