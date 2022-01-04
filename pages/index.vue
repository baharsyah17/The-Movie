<template>
  <div class="bg-black">
    <div class="px-4 py-10 lg:px-20 md:px-10">
      <h1 class="text-center text-3xl font-bold text-white mb-10">
        Now on Cinema
      </h1>
      <div
        class="grid grid-cols-1 cursor-pointer lg:grid-cols-4 lg:gap-10 md:grid-cols-3 md:gap-10 sm:grid-cols-2 sm:gap-5"
      >
        <Movie
          v-for="(movie, id) in results"
          :key="id"
          :results="movie"
          @clickMovie="toPageDetail"
        />
      </div>
      <center><Button @click="addMore" /></center>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Movie from "~/components/mollecules/Movie";
import Button from "~/components/atoms/Button";
export default {
  name: "IndexPage",
  components: { Movie, Button },
  data() {
    return {
      results: [],
      page: 1,
    };
  },
  mounted() {
    this.getDataFromMovieTV();
  },
  methods: {
    getDataFromMovieTV() {
      var api = `https://api.themoviedb.org/3/movie/now_playing?api_key=6de3c0f0176c22fabe34c6be66fa8cae&page=${this.page}`;
      axios
        .get(api)
        .then((res) => {
          res.data.results.forEach((element) => {
            this.results.push(element);
          });
        })
        .catch((err) => console.log(err));
    },
    toPageDetail(movie) {
      this.$router.push(`/detail?id=${movie.id}`);
    },
    addMore() {
      this.page += 1;
      this.getDataFromMovieTV();
    },
  },
};
</script>
