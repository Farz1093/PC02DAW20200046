<template>
  <q-form @submit="applyFilters">
    <q-input v-model="query" label="Search movies" outlined />
    <q-select
      v-model="sort_by"
      :options="sortOptions"
      label="Sort by"
      outlined
    />
    <q-btn type="submit" label="Apply Filters" color="primary" />
  </q-form>
</template>

<script>
export default {
  data() {
    return {
      query: "",
      sort_by: "popularity.desc",
      sortOptions: [
        { label: "Menos Populares", value: "popularity.desc" },
        { label: "Más Populares", value: "popularity.asc" },
        { label: "Menor Rating", value: "vote_average.desc" },
        { label: "Mayor Rating", value: "vote_average.asc" },
      ],
    };
  },
  methods: {
    applyFilters(event) {
      event.preventDefault();
      this.$emit("filters-changed", {
        query: this.query,
        sort_by: this.sort_by,
      });
    },
  },
};
</script>
