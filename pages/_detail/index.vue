<template>
  <div>
    <div>
      <img
        :src="`http://image.tmdb.org/t/p/w500${poster_path}`"
        alt="image not found"
      />
      <h1>{{ title }}</h1>
      <p>Release Date: {{ release_date }}</p>
      <!-- <p v-for="(name, id) in genre" :key="id">Genre: {{ genre.name }}</p> -->
      <p>Run Time: {{ runtime }}</p>
      <p>{{ overview }}</p>
      <!-- <p>{{ production_companies.name }}</p> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      movieId: "",
      param: "",
      poster_path: "",
      title: "",
      release_date: "",
      name: "",
      overview: "",
    };
  },
  mounted() {
    this.getDataDetailMovieTV();
    this.getParam();
  },
  methods: {
    getDataDetailMovieTV() {
      this.movieId = this.$route.query.id;
      var api = `https://api.themoviedb.org/3/movie/${this.movieId}?api_key=6de3c0f0176c22fabe34c6be66fa8cae`;
      axios
        .get(api)
        .then((res) => {
          this.results = res.data.results;
          console.log(this.results);
        })
        .catch((err) => console.log(err));
    },
    getParam() {
      console.log(this.$route);
      this.param = this.$route.params.detail;
      this.movieId = this.$route.query.id;
      // this.poster_path = this.$route.query.poster_path;
      // this.title = this.$route.query.title;
      // this.release_date = this.$route.query.release_date;
      // this.name = this.$route.query.name;
      // this.overview = this.$route.query.overview;
    },
  },
};
</script>

<style></style>
