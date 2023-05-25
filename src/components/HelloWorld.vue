<script>
import axios from "axios"
import { store } from '../data/store';

export default {
  name: "HelloWorld",
  store,
  data() {
    return {
      movieApiList: ' https://api.themoviedb.org/3/discover/movie',
      key: '?api_key=9733f8fbead6e5ca09b6908231558d46',
      imgSrcPath: 'https://www.themoviedb.org/t/p/w440_and_h660_face',
      store
    }
  },
  methods:
  {
    getApyFilm() {
      axios.get(this.movieApiList + this.key)
        .then(r => {
          this.store.film = (r.data)
          console.log(r.data)
          console.log(store.film.results)
        })
    },
    consoleFilm() {
      console.log('ciao' + this.store.film)
    },
  },
  mounted() {
    this.getApyFilm()
  }
}

</script>

<template>
  <div class="main">
    <div>
      <div>

      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main {
  max-width: 1400px;
  margin: 0 auto;
  background-color: rgba(0, 0, 0, 0.474);
  height: 100vh;
}
</style>
