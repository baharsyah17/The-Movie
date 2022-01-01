<template>
  <div class="bg-black">
    <div class="px-20 py-10">
      <h1 class="text-center text-3xl font-bold text-white mb-10">
        Now on Cinema
      </h1>
      <div class="grid grid-cols-4 gap-10">
        <Movie
          v-for="(movie, id) in results"
          :key="id"
          :results="movie"
          @clickMovie="toPageDetail"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Movie from "~/components/mollecules/Movie";
export default {
  name: "IndexPage",
  components: { Movie },
  data() {
    return {
      results: [],
    };
  },
  mounted() {
    this.getDataFromMovieTV();
  },
  methods: {
    getDataFromMovieTV() {
      var api =
        "https://api.themoviedb.org/3/movie/now_playing?api_key=6de3c0f0176c22fabe34c6be66fa8cae&page=1";
      axios
        .get(api)
        .then((res) => {
          this.results = res.data.results;
          console.log(this.results);
        })
        .catch((err) => console.log(err));
    },
    toPageDetail(movie) {
      this.$router.push(`/${movie.title}?id=${movie.id}`);
    },
  },
};
</script>
