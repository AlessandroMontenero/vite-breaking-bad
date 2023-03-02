<script>
export default { 
  data() {
    return {
      name: '',
    }
  },
    methods: {
        search() {
            console.log('ciao')
        },
        handleChange (event) {
              this.$emit("request", event.target.value)
          }
    }
}
</script>
<template>

    <div class="searchBar">
        <input type="text" name="" id="" v-model="name" @input="handleChange">
    <ul>
        <li>
            Monster
        </li>
        <li>
            Spell
        </li>
        <li>
            Trap
        </li>
    </ul>
    </div>
</template>
<style lang="scss" scoped>
.searchBar {
    align-items: stretch;
    display: flex;
    box-sizing: border-box;
    width: 65vw;
    margin: auto;
    padding-bottom: 3rem;
    background-color: white;
    z-index: 2;
    ul {
        list-style: none;
        display: flex;
        height: 100%;
        margin: 0;
        padding: 0;
        li {
            border: 1px solid black;
            border-left: none;
            padding: 1rem;
        }
        li:last-of-type {
            border-radius: 0 10px 10px 0;
        }

    }
    input {
        width: 100%;
        padding: 0 1rem;
        border-radius: 10px 0 0 10px;
        border: 1px solid black;
    }
}
</style>