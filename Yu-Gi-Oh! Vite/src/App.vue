<script>
import cardContainer from './components/cardContainer.vue'

export default {
  components: {
    cardContainer,
  }
}
</script>

<template>
  <cardContainer />

</template>

<style>
  html, body {
    background-color: 	#c0daff;
    font-family: 'Overpass', sans-serif;
    background-image: url();
  }

  body {
    height: 90vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .container {
    width: 100%;
    margin: 0 auto;
    display: flex;
    gap: 1rem;
    flex-direction: column;
    background-color: white;
}
</style>
