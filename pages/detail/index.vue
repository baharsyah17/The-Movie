<template>
  <div class="w-screen place-items-center p-20">
    <nuxt-link
      to="/"
      class="bg-indigo-400 text-white text-center rounded-lg px-16 py-3 cursor-pointer"
      >Back</nuxt-link
    >
    <div
      class="grid grid-cols-1 gap-0 lg:grid-cols-4 gap-10 md:grid-cols-3 gap-10 sm:grid-cols-1 gap-5"
    >
      <div class="mt-20 lg:col-span-2">
        <center>
          <img
            :src="`http://image.tmdb.org/t/p/w500${results.poster_path}`"
            alt="image not found"
            class="rounded-lg"
          />
        </center>
      </div>
      <div class="mt-20 lg:col-span-2 mr-40 md:col-span-2 mr-5">
        <h1 class="font-bold text-6xl">{{ results.title }}</h1>
        <p class="mt-10 text-xl">
          Release Date: <strong> {{ results.release_date }} </strong>
        </p>
        <div>
          <p class="text-xl">
            Genre:
            <strong>
              <span v-for="jenis in tipe.genres" :key="jenis">
                {{ jenis.name }},</span
              >-</strong
            >
          </p>
        </div>
        <p class="text-xl">
          Run Time: <strong> {{ results.runtime }}m </strong>
        </p>
        <p class="mt-10 text-xl mb-15">{{ results.overview }}</p>
        <div class="mt-10 mb-10 border-4 h-0"></div>
        <p class="mt-15 text-xl mb-15">
          Production Studio:
          <br />
          <strong>
            <span v-for="company in tipe.production_companies" :key="company">
              {{ company.name }},</span
            >-</strong
          >
        </p>
        <p class="mt-10 text-xl mb-15">
          Stars:
          <br />
          <strong>
            <span v-for="star in credit" :key="star"> {{ star.name }},</span
            >-</strong
          >
        </p>
        <div class="mt-10 border-4 h-0"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      results: {},
      tipe: {},
      credit: {},
      movieId: "",
      param: "",
    };
  },
  mounted() {
    this.getDataDetailMovieTV();
    this.getDataGenreMovieTV();
    this.getDataCreditsMovieTV();
  },
  methods: {
    getDataDetailMovieTV() {
      this.movieId = this.$route.query.id;
      var api = `https://api.themoviedb.org/3/movie/${this.movieId}?api_key=6de3c0f0176c22fabe34c6be66fa8cae`;
      axios
        .get(api)
        .then((res) => {
          this.results = res.data;
          console.log(this.results);
        })
        .catch((err) => console.log(err));
    },
    getDataGenreMovieTV() {
      var api2 = `https://api.themoviedb.org/3/movie/${this.movieId}?api_key=6de3c0f0176c22fabe34c6be66fa8cae`;
      axios
        .get(api2)
        .then((res) => {
          this.tipe = res.data;
          console.log(this.tipe);
        })
        .catch((err) => console.log(err));
    },
    getDataCreditsMovieTV() {
      var api3 = `https://api.themoviedb.org/3/movie/${this.movieId}/credits?api_key=6de3c0f0176c22fabe34c6be66fa8cae`;
      axios
        .get(api3)
        .then((res) => {
          this.credit = res.data.cast.splice(0, 10);
          console.log(this.credit);
        })
        .catch((err) => console.log(err));
    },
    getParam() {
      console.log(this.$route);
      this.param = this.$route.params.detail;
      this.movieId = this.$route.query.id;
    },
  },
};
</script>

<style></style>
