
<script>
import axios from 'axios'
import card from './card.vue'
export default {
    data() {
        return{
            newCard: [],
            cardsArray: [],
        }
    },
    components: {
        card
    },
    created() {
        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?&num=1&offset=184')
        .then((response) => {
            this.newCard = response.data.data[0]
            this.cardsArray.push(this.newCard)
        })
    }

}

</script>

<template>
    <div class="container">
        <div v-for="card in cardsArray">
            <card :data="card"/>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .container {
        width: 60%;
        margin: 1rem auto;
    }
</style>