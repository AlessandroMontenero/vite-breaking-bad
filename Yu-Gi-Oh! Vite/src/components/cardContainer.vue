
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
        for (let i = 0; i<20; i++){
            let arrayPosition = 0
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?&language=it&num=1&offset=' + i)
            .then((response) => {
                this.newCard = response.data.data[0]
                this.cardsArray.push(this.newCard)
            })
        }
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
        margin: 5rem auto;
        display: flex;
        flex-direction: column;
        background-color: white;
        padding: 2rem;
        border: 4px solid #c8cbb0;
    }
</style>