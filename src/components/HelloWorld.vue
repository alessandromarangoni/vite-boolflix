<script>
import axios from "axios"
import { store } from '../data/store';
export default {
  name: "HelloWorld",
  store,
  data() {
    return {
      movieApiList: ' https://api.themoviedb.org/3/discover/movie',
      tvApiList: ' https://api.themoviedb.org/3/discover/tv',
      imgSrcPath: 'https://image.tmdb.org/t/p/w342/',
      key: '?api_key=9733f8fbead6e5ca09b6908231558d46',
      store
    }
  },
  methods:
  {
    consoleFilm() {
      console.log('ciao' + this.store.film)
    },
    popularsFilm() {
      axios.get(`${this.movieApiList}${this.key}`)
        .then(r => {
          this.store.film = (r.data.results)
          console.log(`${this.movieApiList}${this.key}`)
          console.log(this.store.film)
          console.log(this.store.film[0].title)
        })
    },
    popularsTv() {
      axios.get(`${this.tvApiList}${this.key}`)
        .then(r => {
          this.store.serie = (r.data.results)
          console.log(`${this.tvApiList}${this.key}`)
          console.log(this.store.serie)
          console.log(this.store.serie[0].name)
        })
    }
  }
  , mounted() {
    this.popularsFilm()
    this.popularsTv()
  }
}

</script>

<template>
  <div class="main">
    <div class="container">
      <div class="row">
        <h2>Film</h2>
        <div class=" items_container ">
          <div class="items_wrapper">
            <template v-for="(item) in this.store.film">
              <div class="oggetto">
                <div class="cover">
                  <img class="cover_img" :src="this.imgSrcPath + item.poster_path" :alt="item.title" />
                </div>
                <div class="title"> <strong>Titolo:</strong> {{ item.title }}</div>
                <div class="title"> <strong>Titolo originale:</strong> {{ item.original_title }}</div>
                <img :src="`https://unpkg.com/language-icons@0.2.0/icons/${item.original_language}.svg`" alt="lang"
                  class="language_img">
                <p>{{ item.overview }}</p>
                <template class="vote_container" v-for="voti in Math.ceil(item.vote_average / 2)">
                  <i class="fa-regular fa-star"></i>
                </template>
              </div>
            </template>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <h2>Serie TV</h2>
        <div class="items_container">
          <div class="items_wrapper">
            <template v-for="(item) in this.store.serie">
              <div class="oggetto">
                <div class="cover">
                  <img class="cover_img" :src="`https://image.tmdb.org/t/p/w342/${item.poster_path}`" alt="">
                </div>
                <div class="title"><strong>Titolo:</strong>{{ item.name }}</div>
                <div class="title"><strong>Titolo originale:</strong>{{ item.original_name }}</div>
                <img :src="`https://unpkg.com/language-icons@0.2.0/icons/${item.original_language}.svg`" alt="lang"
                  class=" language_img">
                <template class="vote_container" v-for="voti in Math.ceil(item.vote_average / 2)">
                  <i class="fa-regular fa-star"></i>
                </template>
                <p>{{ item.overview }}</p>
              </div>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.items_container {
  color: white;
}

.main {
  background: rgb(0, 0, 0);
  background: radial-gradient(circle, rgba(0, 0, 0, 1) 5%, rgba(217, 0, 0, 1) 100%);
}

.items_container {
  width: 100%;
  display: flex;
  flex-direction: row;
}

.row {
  width: 100%;
  // background-color: rgba(0, 0, 0, 0.8);
  color: white;

  h2 {
    padding: 1rem;
  }
}


.items_wrapper {
  padding-left: 1rem;
  align-items: center;
  width: 100%;
  min-height: 200px;
  overflow-x: auto;
  display: flex;
  gap: 1.5rem;
  justify-content: space-between;
  padding-bottom: 2rem;
}

.oggetto {
  position: relative;
  // background-color: rgba(0, 0, 0, 0.5);
  min-width: 200px;
  min-height: 300px;
}

p {
  padding: .3rem .5rem;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.title {
  padding: .3rem .5rem;
}

.cover {
  position: absolute;
  min-width: 200px;
  height: 300px;
  background-image: url(https://www.corrierenerd.it/wp-content/uploads/2022/02/png-transparent-video-camera-graphic-film-cinema-movie-projector-camera-camera-lens-text-camera-icon-1-740x813.png);
  background-size: cover;
  object-fit: cover;

  &:hover {
    opacity: 0;
  }

  .cover_img {
    width: 100%;
    height: 100%;
  }
}

.vote_container div {
  display: flex;
  flex-direction: row;

}

.fa-star {
  padding: .3rem .5rem;
}

.language_img {
  width: 30px;
  position: absolute;
  bottom: 0px;
  right: 0px
}
</style>
