<script>
import axios from "axios";
import { store } from '../data/store'
import "/node_modules/flag-icons/css/flag-icons.min.css";
export default {
    name: 'headerApp',
    data() {
        return {
            store,
            apySearchMovie: 'https://api.themoviedb.org/3/search/movie',
            apySearchTv: 'https://api.themoviedb.org/3/search/tv',
            searchtext: '',
            key: '?api_key=9733f8fbead6e5ca09b6908231558d46'
        }
    },
    methods: {
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
    // created() {

    // }

</script>

<template>
    <nav>
        <div class="container">
            <div><img src="https://www.giuseppecaprotti.it/2019/wp-content/uploads/Netflix-Logo.png" alt=""></div>
            <div>
                <input type="text" v-model="this.searchtext" @keyup.enter="search(this.apySearchMovie)"
                    placeholder="quello che cerchi" class="searchbar">
                <button @click="search(this.apySearchMovie)">cerca</button>
            </div>
        </div>
    </nav>
</template>
<style scoped lang="scss">
.container {
    display: flex;
    width: 100%;
    background-color: black;
    justify-content: space-between;
    align-items: center;

    img {
        width: 200px;
    }
}

.searchbar {
    width: 250px;
    height: 1.5rem;
    border-radius: 5px;
    margin-right: 1rem;
    border: 0;
}

button {
    border: 1px solid white;
    border-radius: 15px;
    padding: .25rem .5rem;
    color: white;
    background-color: black;
}
</style>
