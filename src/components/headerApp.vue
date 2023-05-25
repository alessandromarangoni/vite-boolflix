<script>
import axios from "axios";
import { store } from './data/store'
export default {
    name: 'headerApp'
    ,
    data() {
        return {
            store,
        }
    }
}
</script>

<template>
    <nav>
        <div class="container">
            <div><input type="text">quello che cerchi</div>
            <div>
                <button>cerca</button>
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
