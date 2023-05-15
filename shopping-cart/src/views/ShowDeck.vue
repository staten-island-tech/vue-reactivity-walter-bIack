<template>
  <div class="total">
    
    <p class="elixer">
      Average Elixer:
      {{
        deck.length > 0
          ? Math.round(
              (deck.map((value) => value.elixirCost).reduce((acc, value) => acc + value, 0) /
                deck.length) *
                10
            ) / 10
          : 0
      }}
    </p>
    <RouterLink to="/">
      <button class="btn-clash two">
        <div class="overlay"></div>
        <div class="overlay"></div>
        <div class="overlay"></div>
        <span>Home</span>
      </button>
    </RouterLink>
    <div class="parent">
      <div v-for="(card, index) in deck" :key="index" :class="'pos' + index + ' main'">
        <img :src="card.imgUrl" :alt="'Image of ' + card.name" />
        <h1>{{ card.name }}</h1>
        <p>Rarity: {{ card.rarity }}</p>
        <p>Elixir: {{ card.elixirCost }}</p>
        <button class="btn-clash one" @click="remove(card)">
          <div class="overlay"></div>
          <div class="overlay"></div>
          <div class="overlay"></div>
          <span>Remove</span>
        </button>
      </div>
      <img v-for="img in empty.slice(deck.length)" src="../assets/card_blank.webp" alt="black card" 
      :class="'empty pos' + img">
    </div>
  </div>
</template>
<script>
import { RouterLink } from 'vue-router'
import List from '../components/List.vue'

export default {
  components: [List],
  data() {
    return {
      deck: [],
      empty: [1,2,3,4,5,6,7,8]
    }
  },
  methods: {
    remove(card) {
      this.deck = this.deck.filter((deckCard) => deckCard.name !== card.name)
      if (this.deck.length === 0) {
        localStorage.removeItem('deck')
        return
      }
      localStorage.setItem('deck', JSON.stringify(this.deck))
    }
  },
  mounted() {
    let storage = localStorage.getItem('deck')
    if (storage !== null) {
      this.deck = JSON.parse(storage)
    }
  }
}
</script>
<style scoped>
@font-face {
  font-family: 'Clash';
  src: url('../assets/CR.woff2') format('woff2');
}

body {
  font-family: Clash;
}
.total {
  color: rgb(116, 88, 4);
  background-color: #50b1fe;
  box-shadow: 15px 10px #3679af;
  margin-top: 2rem;
  padding-left: 1rem;
  border-radius: 20px;
  height: fit-content;
  text-align:center;
}

.elixer {
  display: inline-block;
  font-size: 2.2rem;
}

.parent {
  display: grid;
  grid-template:
    '1 2 3 4'
    '5 6 7 8';
}

.pos1 {
  grid-area: '1';
}
.pos2 {
  grid-area: '2';
}
.pos3 {
  grid-area: '3';
}
.pos4 {
  grid-area: '4';
}
.pos5 {
  grid-area: '5';
}
.pos6 {
  grid-area: '6';
}
.pos7 {
  grid-area: '7';
}
.pos8 {
  grid-area: '8';
}
.empty {
  margin-top: 15px;
  width:300px;
  height: 450px;
}
.main {
  margin: 1rem 0.5rem;
  width: 275px;
  text-align: center;
  height: 450px;
  background-color: #c4c4c4;
  border-radius: 10px;
  box-shadow: 15px 10px rgb(128, 128, 128);
  padding: 2rem 0rem;
  grid-template-rows: 1;
}
img {
  height: 200px;
}
p {
  margin-bottom: 0.5rem;
}

h1 {
  margin-bottom: 0.5rem;
  font-size: 20px;
}
.btn-clash.one {
  width: 150px;
  border: none;
  border-radius: 5px;
  font-family: inherit;
  font-size: 16px;
  color: inherit;
  background: none;
  cursor: pointer;
  padding: 12px 10px;
  display: inline-block;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 700;
  outline: none;
  position: relative;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;
  background: #ffbd21;
  color: #fff;
  box-shadow: 0 6px #ae6a06, -1px 8px 0 black, 0 0 0 2px black, 0px 6px 0px 2px black;
  -webkit-transition: none;
  -moz-transition: none;
  transition: none;
}
.btn-clash.one:after {
  content: '';
  position: absolute;
  z-index: -1;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;
}
.btn-clash.one:hover {
  box-shadow: 0 4px #ae6a06, 0 0 0 2px black, 0px 4px 0px 2px black;
  top: 2px;
}
.btn-clash.one:active {
  box-shadow: 0 0 #ae6a06, 0 0 0 2px black, 0px 0px 0px 2px black;
  top: 6px;
}
.btn-clash.one .overlay {
  width: 95%;
  height: 87%;
  position: absolute;
  background: rgba(255, 255, 255, 0.08);
  box-shadow: 0px 1px 4px #fe8d0a;
  border-radius: 5px;
  top: 2px;
  left: 5px;
}
.btn-clash.one .overlay + .overlay {
  height: 45%;
  width: 92.5%;
  border-radius: 5px;
  top: 6px;
  background: rgba(255, 255, 255, 0.2);
  box-shadow: none;
}
.btn-clash.one .overlay + .overlay + .overlay {
  width: 5px;
  height: 8px;
  background: rgba(255, 255, 255, 0.65);
  border-radius: 200px;
  right: 8px;
  left: auto;
  -moz-transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
.btn-clash.two {

  width: 150px;
  height: 50px;
  border: none;
  border-radius: 5px;
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  background: none;
  cursor: pointer;
  padding: 12px 10px;
  display: inline-block;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 700;
  outline: none;
  position: relative;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;
  background: #50b1fe;
  color: #fff;
  box-shadow: 0 6px #005cc1, -1px 8px 0 black, 0 0 0 2px black, 0px 6px 0px 2px black;
  -webkit-transition: none;
  -moz-transition: none;
  transition: none;
}
.btn-clash.two:after {
  content: '';
  position: absolute;
  z-index: -1;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;

}
.btn-clash.two:hover {
  box-shadow: 0 4px #005cc1, 0 0 0 2px black, 0px 4px 0px 2px black;
  top: 2px;

}
.btn-clash.two:active {
  box-shadow: 0 0 #005cc1, 0 0 0 2px black, 0px 0px 0px 2px black;
  top: 6px;

}
.btn-clash.two .overlay {
  width: 95%;
  height: 87%;
  position: absolute;
  background: rgba(255, 255, 255, 0.08);
  box-shadow: 0px 1px 4px #2082ff;
  border-radius: 5px;
  top: 2px;
  left: 5px;
}
.btn-clash.two .overlay + .overlay {
  height: 45%;
  width: 92.5%;
  left: 7px;
  border-radius: 5px;
  top: 6px;
  background: rgba(255, 255, 255, 0.2);
  box-shadow: none;
}
.btn-clash.two .overlay + .overlay + .overlay {
  width: 5px;
  height: 8px;
  background: rgba(255, 255, 255, 0.65);
  border-radius: 200px;
  right: 8px;
  left: auto;
  -moz-transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
</style>
