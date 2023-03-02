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
      img_cropped: '',
      color: '',
      values: []
    }
  },
  created() {
        let card = this.data
        this.name = card.name
        this.desc = card.desc
        this.img_cropped = card.card_images[0].image_url_cropped
        this.img = card.card_images[0].image_url
        this.attribute = card.attribute
        this.race = card.race
        if (card.type.includes('Monster')) {
          this.color = 'monster'
          this.level = card.level
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
        <img v-if="(attribute != 'Spell') && (attribute != 'Trap')" :src="'src/img/attributeIcons/' + attribute + '.png'" alt="">
        <img v-else-if="attribute == 'Spell'" src="src/img/attributeIcons/spell.svg" alt="">
        <img v-else-if="attribute == 'Trap'" src="src/img/attributeIcons/Trap.svg" alt="">
        {{ attribute }}
        <img v-if="(attribute != 'Spell') && (attribute != 'Trap')" src="src/img/attributeIcons/star.png" alt="">
        <span v-if="(attribute != 'Spell') && (attribute != 'Trap')" > LEVEL {{ level }}</span>
        <span v-if="(attribute != 'Spell') && (attribute != 'Trap')" class="attributes">[ 
          <span v-for="(value, index) in values" >
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
    
    <div class="background" :style="'background-image: url(' + img_cropped + ');'"></div>
  </div>
</template>

<style lang="scss" scoped>
.card:hover {
  ::-webkit-scrollbar {
    width: 5px;
  }
  ::-webkit-scrollbar-track {
    background: none;
  }
  
  aspect-ratio: 3.5 / 1;
  .cardImg {
    height: 0;
    width: 0;
    padding: 0;
  }
  
  .cardDetails {
    height: 100%;
    padding: 10px;
    box-sizing: border-box;
    .stats, .name {
      margin-right: 0;
    }
  }


  .cardDetails .description {
    overflow: auto;
    height: fit-content;
    margin: 0;
  }

  .background {
    opacity: 1;
    position: relative;
    filter: blur(0);

  }
  .background::before {
    width: 80%;    
    background: none;
  }
}
.card  .background {
  position: absolute;
  bottom: 0;
  right: 0;
  height: 100%;
  aspect-ratio: 1 / 1;
  z-index: 0;
  opacity: .04;
  background-size: contain;
  background-position: right;
  background-repeat: no-repeat;
  transition: all .2s linear;
  border-radius: 0 15px 15px 0;
}
.background::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(to left, rgba(0,0,0,0), rgba(0,0,0,0), white);
  transition: all .1s linear;
}
.card {
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  position: relative;
  aspect-ratio: 5 / 1;
  transition: all .1s linear;
  border-radius: 15px;
  gap: 10px;
  &.monster {
    background: linear-gradient(to top left, rgba($color: #FDE68A, $alpha: .2), rgba($color: #FDE68A, $alpha: .5));
    border-bottom: 5px solid #FDE68A;
    ::-webkit-scrollbar-thumb {
      background: #FDE68A;
    }
  }
  &.spell {
    background: linear-gradient(to top left, rgba($color: #1D9E74, $alpha: .2), rgba($color: #1D9E74, $alpha: .5));
    border-bottom: 5px solid #1D9E74;
    ::-webkit-scrollbar-thumb {
      background: #1D9E74;
    }
  }
  &.trap {
    background: linear-gradient(to top left, rgba($color: #BC5A84, $alpha: .2), rgba($color: #BC5A84, $alpha: .5));
    border-bottom: 5px solid #BC5A84;
    ::-webkit-scrollbar-thumb {
      background: #BC5A84;
    }
  }
  .cardImg {
    height: 100%;
    padding: .6rem;
    box-sizing: border-box;
    z-index: 1;
    transition: all .1s linear;
    img {
      height: 100%;
      border-radius: 5px;
    }
  }
  .cardDetails {
    z-index: 1;
    width: 100%;
    display: flex;
    flex-direction: column;
    padding: 10px;
    .name, .stats {
      margin: 0 1rem;
      line-height: 2.2rem;
      border-bottom: 1px solid rgba(0, 0, 0, .4);
      box-sizing: border-box;
      font-weight: 600;
      text-transform: uppercase;
    }
    .name {
      font-size: 1.3rem;
    }
    
    .stats {
      display: flex;
      gap: 10px;
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      .attributes {
        margin-right: auto;
      }
      .values {
        margin-left: auto;
        margin-right: 1rem;
      }
      img {
        height: 20px;
      }
    }
    .description {
      padding: .5rem 1rem;
      overflow: hidden;
      font-style: italic;
      transition: all .1s linear;
    }
  }
}
</style>
