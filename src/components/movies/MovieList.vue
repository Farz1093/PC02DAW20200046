<template>
  <q-card class="movie-list">
    <q-img :src="posterUrl" alt="Poster" class="movie-poster" />
    <q-card-section>
      <div class="text-h6">{{ title }}</div>
      <div>Rating: {{ vote_average }} ({{ vote_count }} votes)</div>
    </q-card-section>
  </q-card>
</template>

<style>
.movie-card {
  max-width: 100px;
  margin: 10px;
}
.movie-poster {
  height: 450px;
  max-width: 250px;
  object-fit: cover;
  border-radius: 8px;
  margin: 0 auto;
}
</style>

<script>
export default {
  props: {
    title: { type: String, required: true },
    poster_path: { type: String, required: true },
    vote_average: { type: Number, required: true },
    vote_count: { type: Number, required: true },
  },
  computed: {
    posterUrl() {
      return `http://image.tmdb.org/t/p/w500${this.poster_path}`;
    },
  },
};
</script>
