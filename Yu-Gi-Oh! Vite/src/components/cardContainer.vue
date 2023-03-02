
<script>
import axios from 'axios'
import { toRaw } from 'vue'
import card from './card.vue'
export default {
    data() {
        return{
            cardsArray: [],
            page: 0,
            name: ''
        }
    },
    components: {
        card
    },
    created() {
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?&language=it&num=15&offset=' + this.page)
            .then((response) => {
                for (let newCard of response.data.data) {
                    console.log(response.data)
                    this.cardsArray.push(newCard)
                }
            })
    },
    methods: {
        search() {
            this.cardsArray = []
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?fname=' + this.name + '&language=it&num=15&offset=' + this.page)
            .then((response) => {
                for (let newCard of response.data.data) {
                    console.log(response.data.meta)
                    this.cardsArray.push(newCard)
                }
            })
        }
    }

}

</script>

<template>
    <main>
        <div class="container">
            <input type="text" name="" id="" v-model="name" v-on:change="search()">
            <button @click="search()"></button></div>
        <div class="container">
            
            <div v-for="card in cardsArray">
                <card :data="card"/>
            </div>
        </div>
    </main>
</template>

<style lang="scss" scoped>
main {
    padding: 3rem;
    width: 65vw;
    margin: auto;
    margin-top: 5%;
    height: 80vh;
    overflow-y: auto;
    background-color: white;
    display: flex;
    flex-direction: column;
    gap: 3rem;
}

::-webkit-scrollbar {
    width: 5px;
    left: 50px;
    position: fixed;
}
::-webkit-scrollbar-track {
    background: none;
    
}
::-webkit-scrollbar-thumb {
    background: #FDE68A;
    border-radius: 50px;
  }
</style>