<template>
  <div class="home">
    <img alt="Batman logo" src="../assets/logo.png" />
    <HelloWorld v-bind:msg="'Hello ' + user.name +', which batman movie do you want to see?'"/>
    <MovieList />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import MovieList from '@/components/MovieList.vue';
import { mapState } from 'vuex';

export default {
  name: 'Home',
  components: {
    HelloWorld,
    MovieList,
  },
  computed: {
    ...mapState(['user']),
  },
};
</script>
