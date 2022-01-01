<template>
  <div>
    <div @click="$emit('clickMovie', results)">
      <img
        :src="`http://image.tmdb.org/t/p/w500${results.poster_path}`"
        alt="image not found"
        class="w-3/4 m-5"
      />
      <p class="m-5 text-white">
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
