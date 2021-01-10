<template>
  <header>
    <router-link to="/">
      <h1 class="text-center">Vue<span>Movies</span>Api</h1>
    </router-link>
  </header>
  <router-view />
</template>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-decoration: none;
}
span {
  color: green;
}

a {
  text-decoration: none;
}
h1 {
  color: white;
  padding: 5px;
  background-color: #000022;
  margin-bottom: -1px;
}
</style>
