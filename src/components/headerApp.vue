<script>
import axios from "axios";
import { store } from '../data/store'
export default {
    name: 'headerApp'
    ,
    data() {
        return {
            store,
            apySearchMovie: 'https://api.themoviedb.org/3/search/movie',
            searchtext: '',
            key: '?api_key=9733f8fbead6e5ca09b6908231558d46'
        }
    },
    methods: {
        search(what) {
            axios.get(`${what}${this.key}&query=${this.searchtext}`)
                .then(r => {
                    this.store.film = (r.data.results)
                    console.log(`${this.apySearch}${this.key}&query=${this.searchtext}`)
                    console.log(this.store.film)
                    console.log(this.store.film[0].title)
                })
        }
    }
}

    // created() {

    // }

</script>

<template>
    <nav>
        <div class="container">
            <div><input type="text" v-model="this.searchtext">quello che cerchi</div>
            <div>
                <button @click="search(this.apySearchMovie)">cerca</button>
            </div>
        </div>
    </nav>
</template>
<style scoped lang="scss">
.container {
    display: flex;
    width: 100%;
    height: 80px;
    background-color: black;
    justify-content: center;
    align-items: center;
}
</style>
