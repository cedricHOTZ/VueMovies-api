<template>
  <div class="home">
    <h5 class="text-center">succes du moment</h5>
    <div class="feature-card ">
      <router-link to="/movie/">
        <img
          src="https://m.media-amazon.com/images/M/MV5BYWFkMTJjODEtMjY2NC00OGRiLThkYjMtMzBjMzVhY2FlZTEyXkEyXkFqcGdeQXVyNjYwMjkwMjg@._V1_SX300.jpg"
          class="featured-img"
        />
        <div class="detail">
          <h3>naruto</h3>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Sapiente
            facilis asperiores excepturi? Animi, quia tempora? Nostrum vero,
            aliquam recusandae nemo error ipsa dolores impedit, voluptatum
            provident ut est, asperiores inventore.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="searchMovies()" class="search-box">
      <input
        type="text"
        placeholder="Entrez un titre de film"
        v-model="search"
      />
      <input type="submit" value="Rechercher" class="btn btn-primary" />
    </form>

    <div class="movies-list">
      <div class="container">
        <div class="row">
          <div
            class="movie col-md-4 mt-4  mb-5"
            v-for="movie in movies"
            :key="movie.imdbI"
          >
            <div class="col-sm-6 col-md-3">
              <router-link :to="'/movie/' + movie.imdbID">
                <div class="product-image">
                  <img :src="movie.Poster" />
                  <!-- <div class="type">{{ movie.Type }}</div> -->
                </div>
                <div class="detail">
                  <h3>{{ movie.Title }}</h3>
                  <p class="">Année: {{ movie.Year }}</p>
                </div>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";
import env from "@/env.js";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);
    const searchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            // console.log(data);
            movies.value = data.Search;
            search.value = "";
          });
      }
    };
    return {
      search,
      movies,
      searchMovies
    };
  }
};
</script>
<style lang="scss" scoped>
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      object-fit: cover;
      height: 300px;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      bottom: 0;
      right: 0;
      z-index: 1;
      padding: 15px;
      overflow: hidden;
      background-color: rgba(0, 0, 0, 0.6);

      h3 {
        color: white;
        text-align: center;
        text-decoration: none;
      }
      p {
        color: white;
        text-decoration: none;
      }
    }
  }
}
.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;

  input {
    display: block;
    appearance: none;
    border: none;
    outline: none;
    background: none;

    &[type="text"] {
      width: 100%;
      color: white;
      background-color: #496583;
      font-size: 20px;
      border-radius: 8px;
      transition: 0.5s;
      margin-bottom: 15px;
      text-align: center;

      &::placeholder {
        color: white;
        text-align: center;
      }
      &::focus {
        box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
      }
    }
    &[type="submit"] {
      width: 100%;
      max-width: 300px;
      background-color: #42b883;
      padding: 16px;
      border-radius: 8px;
      color: white;
      transition: 0.4s;
      text-transform: uppercase;

      &:active {
        background-color: #3b8070;
      }
    }
  }
}
h3 {
  width: max-content;
  margin-top: 2px;
  color: white;
}
p {
  color: white;
}
a {
  text-decoration: none;
}
.movie {
  background-color: rgba(0, 0, 0, 0.2);
}
</style>
