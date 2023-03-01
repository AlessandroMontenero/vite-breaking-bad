<script>
  import axios from 'axios'
export default {
  props: {
    data: Object
  },
  data() {
    return {
      name: '',
      attribute: '',
      level: '',
      type: '',
      race: '',
      atk: '',
      def: '',
      desc: '',
      img: '',
      color: '',
      values: []
    }
  },
  created() {
    console.log(this.data);
        let card = this.data
        this.name = card.name
        this.desc = card.desc
        this.img = card.card_images[0].image_url_cropped
        this.attribute = card.attribute
        if (card.type.includes('Monster')) {
          this.color = 'monster'
          this.level = card.level
          this.race = card.race
          this.type = card.type.replace('Monster', '').replace('Normal', '')
          this.values = this.type.split(' ')
          this.values.unshift(this.race)
          this.atk = card.atk
          this.def = card.def
          
        }
        else if (card.type.includes('Spell')){
          this.color = 'spell'
          this.attribute = 'Spell'
        }
        else if (card.type.includes('Trap')){
          this.color = 'trap'
          this.attribute = 'Trap'
        }
  }
}


</script>

<template>
  
  <div class="card" :class="color">
    <div class="cardImg">
      <img :src="img" alt="">
    </div>
    <div class="cardDetails">
      <div class="name">
        {{ name }}
      </div>
      <div class="stats">
        <img :src="'src/img/attributeIcons/'+ attribute +'.png'" alt="">
        {{ attribute }}
        <img src="src/img/attributeIcons/star.png" alt="">
        <span> LEVEL {{ level }}</span>
        <span v-if="(attribute != 'Spell') && (attribute != 'Trap')">[ 
            <span v-for="(value, index) in values">
              {{ value }} 
              <span v-if="values[index + 1]">/ </span>
            </span>
          ] </span>
        <div class="values" v-if="(attribute != 'Spell') && (attribute != 'Trap')">
          ATK {{ atk }} || DEF {{ def }}
        </div>
      </div>
      <div class="description">
        {{ desc }}
      </div>
    </div>
    
  </div>
</template>

<style lang="scss" scoped>
.card {
  display: flex;
  border-radius: 10px;
  &.monster {
    background-color: rgba($color: #FDE68A, $alpha: .6);
    border: 2px solid white;
    outline: 5px solid #FDE68A;
  }
  &.spell {
    background-color: rgba($color: #1D9E74, $alpha: .6);
    border: 2px solid white;
    outline: 5px solid #1D9E74;
  }
  &.trap {
    background-color: rgba($color: #BC5A84, $alpha: .6);
    border: 2px solid white;
    outline: 5px solid #BC5A84;
  }
  .cardImg {
    height: 11.8rem;
    aspect-ratio: 1 / 1;
    padding: .6rem;
    box-sizing: border-box;
    img {
      width: 100%;
      border-radius: 5px;
    }
  }
  .cardDetails {
    width: 100%;
    .name, .stats {
      padding: .1rem 0;
      margin: 0 .3rem;
      height: 2.2rem;
      line-height: 2.2rem;
      border-bottom: 1px solid rgba(0, 0, 0, .4);
      box-sizing: border-box;
      font-weight: 600;
      text-transform: uppercase;
    }

    .stats {
      display: flex;
      gap: .6rem;
      display: flex;
      align-items: center;
      .values {
        margin-left: auto;
        margin-right: 1rem;
      }
      img {
        height: 20px;
      }
    }
    .description {
      padding: .5rem .3rem;
      box-sizing: border-box;
      height: 6.5rem;
      overflow: hidden;
      font-style: italic;
    }
  }
}
</style>
