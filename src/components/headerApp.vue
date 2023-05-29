<script>
import axios from "axios";
import { store } from '../data/store'
import "/node_modules/flag-icons/css/flag-icons.min.css";
import HelloWorld from './HelloWorld.vue'
export default {
    name: 'headerApp',
    data() {
        return {
            store,
            HelloWorld,
            apySearchMovie: 'https://api.themoviedb.org/3/search/movie',
            apySearchTv: 'https://api.themoviedb.org/3/search/tv',
            searchtext: '',
            movieApiList: ' https://api.themoviedb.org/3/discover/movie',
            key: '?api_key=9733f8fbead6e5ca09b6908231558d46',
            piùVotati: 'https://api.themoviedb.org/3/movie/top_rated',
            linkHeader: ['Film più votati', 'Scopri Film']
        }
    },
    methods: {
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
        },
        searchMovie() {
            axios.get(`${this.apySearchMovie}${this.key}&query=${this.searchtext}`)
                .then(r => {
                    this.store.film = (r.data.results)
                    console.log(`${this.apySearchMovie}${this.key}&query=${this.searchtext}`)
                    console.log(this.store.film)
                    console.log(this.store.film[0].title)
                })
        },
        searchTv() {
            axios.get(`${this.apySearchTv}${this.key}&query=${this.searchtext}`)
                .then(r => {
                    this.store.serie = (r.data.results)
                    console.log(`${this.apySearchTv}${this.key}&query=${this.searchtext}`)
                    console.log(this.store.serie)
                    console.log(this.store.serie[0].name)
                })
        },
        search() {
            this.searchTv();
            this.searchMovie()
        },
    }
}

</script>

<template>
    <nav>
        <div class="container">
            <div class="logo_wrapper">
                <img src="https://www.giuseppecaprotti.it/2019/wp-content/uploads/Netflix-Logo.png" alt="">
            </div>
            <template v-for="item in this.linkHeader">
                <div @click="this.popularsFilm()">{{ item }}</div>
            </template>
            <div>
                <input type="text" v-model="this.searchtext" @keyup.enter="search()" placeholder="quello che cerchi"
                    class="searchbar">
                <button @click="search()">cerca</button>
            </div>
        </div>
    </nav>
</template>
<style scoped lang="scss">
.container {
    display: flex;
    width: 100%;
    background: rgb(0, 0, 0);
    justify-content: space-between;
    align-items: center;
    color: white;

    .logo_wrapper {
        height: 80px;
        object-fit: cover;
    }

    img {
        height: 100%;
    }
}

.searchbar {
    width: 250px;
    height: 1.8rem;
    border-radius: 5px;
    margin-right: 1rem;
    border: 2px solid white;
    background-color: rgba(240, 248, 255, 0);
    color: white;
}

button {
    border: 1px solid white;
    border-radius: 15px;
    padding: .25rem .5rem;
    color: white;
    background-color: black;
}
</style>
