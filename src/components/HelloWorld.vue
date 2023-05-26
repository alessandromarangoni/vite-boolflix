<script>
import axios from "axios"
import { store } from '../data/store';

export default {
  name: "HelloWorld",
  store,
  data() {
    return {
      movieApiList: ' https://api.themoviedb.org/3/discover/',
      imgSrcPath: 'https://www.themoviedb.org/t/p/w440_and_h660_face',
      store
    }
  },
  methods:
  {
    consoleFilm() {
      console.log('ciao' + this.store.film)
    },
  }
}

</script>

<template>
  <div class="main">
    <div>
      <div v-for="(item, i) in this.store.film">
        <h2>{{ item.title }}</h2>
        <h3>{{ item.original_title }}</h3>
        <span> {{ item.original_language }}</span>
        <span>{{ item.vote_average }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main {
  max-width: 1400px;
  margin: 0 auto;


  div {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    div {
      width: calc(100% / 5);
      display: flex;
      flex-direction: column;
      padding-top: 1rem;

      h3 {
        line-height: 1rem;
      }
    }
  }
}
</style>
