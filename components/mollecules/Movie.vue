<template>
  <div>
    <div @click="$emit('clickMovie', results)">
      <center>
        <img
          :src="`http://image.tmdb.org/t/p/w500${results.poster_path}`"
          alt="image not found"
          class="w-3/4 lg:m-5"
        />
      </center>
      <p class="m-5 text-white text-center">
        {{ results.title }} ({{ setYear(results.release_date) }})
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    results: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    setYear(params) {
      return params.substring(0, 4);
    },
  },
};
</script>

<style></style>
