<script>
export default { 
  data() {
    return {
      name: '',
      type: '',
      typeIndex: 4,
    }
  },
    methods: {
        handleChange (event) {
            let newResearch = {
                name: this.name,
                type: this.type
            }
              this.$emit("request", newResearch)
          },
    }
}
</script>
<template>

    <div class="searchBar">
        <input type="text" name="" id="" v-model="name" @input="handleChange">
    <ul>
        <li id="monster" @click="type = 'Normal Monster', handleChange(), typeIndex = 0" :class="{active : (typeIndex == 0)}">
            Monster
        </li>
        <li id="spell" @click="type = 'Spell Card', handleChange(), typeIndex = 1" :class="{active : (typeIndex == 1)}">
            Spell
        </li>
        <li id="trap" @click="type = 'Trap Card', handleChange(), typeIndex = 2" :class="{active : (typeIndex == 2)}">
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
            &#monster.active {
                background-color: #fde68a88;
            }
            &#spell.active {
                background-color: #1d9e737f;
            }
            &#trap.active {
                background-color: #bc5a8480;
            }
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