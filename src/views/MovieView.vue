<template>
  <div v-if="movie" class="movie-view">
    <h1>{{ movie.Title }}</h1>
    <hr />
    <img v-bind:src="movie.Poster" v-bind:alt="movie.Title">
    <div class="movie-description">
      <span><b>imdb:</b> {{ movie.imdbID }}</span>
      <span><b>year:</b> {{ movie.Year }}</span>
      <span><b>type:</b> {{ movie.Type }}</span>
    </div>
  </div>
  <div v-else class="movie-view">Movie is NULL</div>
</template>

<script lang="ts">
import Vue from 'vue';
import MovieService from '@/services/MovieService';
import { Movie } from '@/services/types';

export default Vue.extend({
  name: 'MovieView',
  props: {
    movieId: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      movie: {} as Movie,
    };
  },
  async created() {
    if (this.movieId) {
      const movie = await MovieService.movieService.getSpecificMovie(/* TODO */ '273b9080', this.movieId);
      this.movie = movie;
    }
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .movie-description {
    display: flex;
    flex-direction: column;
  }
</style>
