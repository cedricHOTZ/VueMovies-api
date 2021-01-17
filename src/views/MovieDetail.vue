<template>
  <div class="movie-detail">
    <div class="container">
    <h1 class="text-center mt-5">{{ movie.Title }}</h1>
    <div class="row">
      <div class="col-md-5 col-sm-12 pl-5">
        <img :src="movie.Poster" />
      </div>
      <div class="col-md-6 mt-4">
       
        <p class="mt-3">{{movie.Plot}}</p>
         <p> Année de sortie : {{movie.Year}}</p>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.apiKey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
          // console.log(data))
        });
    });
    return {
      movie
    };
  }
};
</script>

<style lang="scss" scoped></style>
