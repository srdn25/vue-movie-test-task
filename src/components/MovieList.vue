<template>
  <div class="hello">
    <MovieListItem
      v-for="movie in movies"
      :key="movie.imdbID"
      :movie="movie"
      />

    <button @click="() => loadMovies(this.page + 1)">Load more</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import MovieService from '@/services/MovieService';
import MovieListItem from './MovieListItem.vue';
import { Movie } from '../services/types';

export default Vue.extend({
  name: 'MovieList',
  data() {
    return {
      movies: [] as Movie[],
      page: 1,
    };
  },
  async created() {
    await this.loadMovies(this.page);
  },
  methods: {
    async loadMovies(page: number) {
      try {
        this.page = page;
        const result = await MovieService.movieService.getMovieList(/* TODO */ '273b9080', page);
        this.movies = result.result;
      } catch (err) {
        console.error(`Something wrong in request movies. ${err}`);
      }
    },
  },
  components: {
    MovieListItem,
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
