<script>
import axios from "axios"
import { store } from '../data/store';
export default {
  name: "HelloWorld",
  store,
  data() {
    return {
      movieApiList: ' https://api.themoviedb.org/3/discover/',
      imgSrcPath: 'https://image.tmdb.org/t/p/w342/',
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
              <h4>{{ item.title }}</h4>
              <h5>{{ item.original_title }}</h5>
              <img :src="`https://unpkg.com/language-icons@0.2.0/icons/${item.original_language}.svg`" alt="lang"
                class="language_img">
              <p>{{ item.vote_average }}</p>
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
    <h2>Serie TV</h2>
    <div class="row">
      <div class="items_container">
        <div class="items_wrapper">
          <template v-for="(item) in this.store.serie">
            <div class="oggetto">
              <div class="cover">
                <img class="cover_img" :src="`https://image.tmdb.org/t/p/w342/${item.poster_path}`" alt="">
              </div>
              <h4>{{ item.name }}</h4>
              <h5>{{ item.original_name }}</h5>
              <img :src="`https://unpkg.com/language-icons@0.2.0/icons/${item.original_language}.svg`" alt="lang"
                class=" language_img">
              <p>{{ item.vote_average }}</p>
              <template class="vote_container" v-for="voti in Math.ceil(item.vote_average / 2)">
                <i class="fa-regular fa-star"></i>
              </template>
            </div>
          </template>

        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.items_container {
  color: white;
}

.items_container {
  width: 100%;
  display: flex;
  flex-direction: row;
}

.row {
  width: 100%;
  background-color: rgba(0, 0, 0, 0.459);
}


.items_wrapper {
  align-items: center;
  width: 100%;
  height: 500px;
  background-color: red;
  overflow-x: scroll;
  display: flex;
  gap: 2rem;
  justify-content: space-between;
}

.oggetto {
  position: relative;
  background-color: rgba(0, 0, 0, 0.459);
  min-width: 200px;
  min-height: 300px;

  h4,
  h5,
  p {
    padding: 1rem;
  }

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
  padding-left: .5rem;
}

.language_img {
  width: 30px;
  position: absolute;
  bottom: 0px;
  right: 0px
}
</style>
