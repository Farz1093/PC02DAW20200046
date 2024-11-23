<template>
  <q-page class="q-pa-md">
    <!-- Filtro de películas -->
    <movie-filter @filters-changed="updateFilters" />

    <!-- Mostrar lista de películas -->
    <q-card-grid cols="4" class="q-mt-md">
      <movie-list
        v-for="movie in movies"
        :key="movie.id"
        :title="movie.title"
        :poster_path="movie.poster_path"
        :vote_average="movie.vote_average"
        :vote_count="movie.vote_count"
      />
    </q-card-grid>

    <!-- Paginación -->
    <q-pagination
      v-model="page"
      :max="total_pages"
      @update:model-value="fetchMovies"
      class="q-mt-lg"
    />
  </q-page>
</template>

<script>
import { discoverMovies } from "src/boot/axios";
import MovieList from "src/components/movies/MovieList.vue";
import MovieFilter from "src/components/movies/MovieFilter.vue";

export default {
  components: { MovieList, MovieFilter },
  data() {
    return {
      movies: [],
      page: 1,
      total_pages: 1,
      filters: { sort_by: "popularity.desc", include_adult: false },
    };
  },
  methods: {
    async fetchMovies() {
      try {
        const response = await discoverMovies({
          ...this.filters,
          page: this.page,
        });
        this.movies = response.results;
        this.total_pages = response.total_pages;
      } catch (error) {
        console.error("Error fetching movies:", error);
      }
    },
    updateFilters(newFilters) {
      this.filters = { ...this.filters, ...newFilters };
      this.page = 1;
      this.fetchMovies();
    },
  },
  created() {
    this.fetchMovies();
  },
};
</script>
