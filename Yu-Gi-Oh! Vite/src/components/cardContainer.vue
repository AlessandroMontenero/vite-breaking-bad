
<script>
import { toRaw } from 'vue'
import card from './card.vue'
export default {
    props: {
        cards: Array
    },
    data() {
        return{
        }
    },
    components: {
        card
    }

}

</script>

<template>
    <main>
        <div class="container">
            <div v-for="card in cards">
                <card :data="card"/>
            </div>
        </div>
    </main>
</template>

<style lang="scss" scoped>
main {
    width: 65vw;
    margin: auto;
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