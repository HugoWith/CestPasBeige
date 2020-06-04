<template>
  <div id="app">
    <!-- <router-link to="/">Home</router-link>| -->
    <!-- <router-link to="/about">About</router-link> -->
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
}

body {
  background: rgb(247, 197, 159);
  background: linear-gradient(
    131deg,
    rgba(247, 197, 159, 1) 75%,
    rgba(254, 234, 0, 1) 100%
  );
  height: 100%;
  width: 100%;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
