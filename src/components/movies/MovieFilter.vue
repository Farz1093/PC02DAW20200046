<template>
  <q-form @submit="applyFilters">
    <q-input v-model="query" label="Search movies" outlined />
    <q-select
      v-model="sort_by"
      :options="sortOptions"
      label="Sort by"
      outlined
    />
    <q-btn
      type="submit"
      label="Apply Filters"
      color="primary"
      @click="applyFilters"
    />
  </q-form>
</template>

<script>
export default {
  data() {
    return {
      query: "",
      sort_by: "popularity.desc",
      sortOptions: [
        { label: "Popularity Desc", value: "popularity.desc" },
        { label: "Popularity Asc", value: "popularity.asc" },
        { label: "Rating Desc", value: "vote_average.desc" },
        { label: "Rating Asc", value: "vote_average.asc" },
      ],
    };
  },
  methods: {
    applyFilters() {
      this.$emit("filters-changed", {
        query: this.query,
        sort_by: this.sort_by,
      });
    },
  },
};
</script>
