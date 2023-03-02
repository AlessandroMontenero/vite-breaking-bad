<script>
import cardContainer from './components/cardContainer.vue'
import searchBar from './components/searchBar.vue'
import axios from 'axios'


export default {
  data() {
    return {
      requestName: '',
      cardsArray: [],
      page: 0,
      name: '',
      searchProxy: {}
    }
  },
  components: {
    cardContainer,
    searchBar,
  },
  methods: {
    handleCustomChange (newResearch) {
          console.log(newResearch)
          this.searchProxy = newResearch
          this.search()
        },
    search() {
      this.cardsArray = []
      let url = 'https://db.ygoprodeck.com/api/v7/cardinfo.php?&language=it&fname='+ this.searchProxy.name + '&num=15&offset=' + this.page
      if (this.searchProxy.type != '')
      {
        url += '&type=' + this.searchProxy.type 
      }
      axios.get(url)
            .then((response) => {
                for (let newCard of response.data.data) {
                    this.cardsArray.push(newCard)
                }
            })
    }
  },
    created() {
      let url = 'https://db.ygoprodeck.com/api/v7/cardinfo.php?&language=it&num=15&offset=0'
      console.log(url)
      axios.get(url)
            .then((response) => {
                for (let newCard of response.data.data) {
                    this.cardsArray.push(newCard)
                }
            })
    }
}
</script>

<template>
  <searchBar @request="handleCustomChange"  />
  <cardContainer :cards="cardsArray"/>

</template>

<style>
  html, body {
    background-color: 	#c0daff;
    font-family: 'Overpass', sans-serif;
    background-image: url();
    margin: 0;
  }


  .container {
    width: 100%;
    margin:  auto;
    display: flex;
    gap: 1rem;
    flex-direction: column;
    background-color: white;
}
</style>
