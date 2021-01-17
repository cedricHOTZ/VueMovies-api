<template>
  <header>
    <router-link to="/">
      <h1 class="text-center">Vue<span>Movies</span>Api</h1>
    </router-link>
  </header>
  <router-view />
</template>

<style scoped lang="scss" >
* {
  margin: 0 !important;
  padding: 0;

  text-decoration: none;
 
}

span {
  color: #42b883;
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
