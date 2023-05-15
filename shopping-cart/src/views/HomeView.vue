<template>
  <main>
    <div class="controlls">
      <button class="btn-clash two" @click="filterClicked">
        <div class="overlay"></div>
        <div class="overlay"></div>
        <div class="overlay"></div>
        <span>{{ sortList[currentFilter] }}</span>
      </button>
      <p class="counter">Deck:{{ deck.length }}/8</p>
      <RouterLink to="/deck">
        <button class="btn-clash two">
          <div class="overlay"></div>
          <div class="overlay"></div>
          <div class="overlay"></div>
          <span>Deck</span>
        </button>
      </RouterLink>
    </div>
    <List :cards="cards" :key="item" @toDeck="(event) => addToDeck(event)" />
  </main>
</template>
<script>
import { RouterLink } from 'vue-router'
import cardsList from '../assets/cards.js'
import List from '../components/List.vue'
export default {
  data() {
    return {
      cards: [],
      deck: [],
      sortList: ['Random', 'By Arena', 'By Elixir', 'By Rarity Descending', 'By Rarity'],
      currentFilter: 0,
      keyRarity: { Champion: 1, Legendary: 2, Epic: 3, Rare: 4, Common: 5 },
      keyArena: {
        'Training Camp': 0,
        'Goblin Stadium': 1,
        'Bone Pit': 2,
        'Barbarian Bowl': 3,
        'Spell Valley': 4,
        "Builder's Workshop": 5,
        "P.E.K.K.A's Playhouse": 6,
        'Royal Arena': 7,
        'Frozen Peak': 8,
        'Jungle Arena': 9,
        'Hog Mountain': 10,
        'Electro Valley': 11,
        'Spooky Town': 12,
        "Rascal's Hideout": 13,
        'Serenity Peak': 14,
        "Miner's Mine": 15,
        "Executioner's Kitchen": 16,
        'Royal Crypt': 17,
        'Silent Sanctuary': 18,
        'Dragon Spa': 19,
        'Legendary Arena': 20
      }
    }
  },
  name: 'home',
  components: {
    List
  },
  methods: {
    shuffle(array) {
      let currentIndex = array.length,
        temporaryValue,
        randomIndex
      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex)
        currentIndex -= 1
        temporaryValue = array[currentIndex]
        array[currentIndex] = array[randomIndex]
        array[randomIndex] = temporaryValue
      }
      return array
    },
    filterClicked() {
      this.currentFilter++
      if (this.currentFilter > 4) this.currentFilter = 0
      switch (this.sortList[this.currentFilter]) {
        case 'By Rarity Descending':
          this.cards.sort((a, b) => this.keyRarity[a.rarity] - this.keyRarity[b.rarity])
          break
        case 'By Rarity':
          this.cards.sort((a, b) => this.keyRarity[b.rarity] - this.keyRarity[a.rarity])
          break
        case 'By Elixir':
          this.cards.sort((a, b) => a.elixirCost - b.elixirCost)
          break
        case 'By Arena':
          this.cards.sort((a, b) => this.keyArena[a.arena] - this.keyArena[b.arena])
          break
        default:
          this.cards = this.shuffle(this.cards)
      }
    },
    addToDeck(card) {
      if (this.deck.length === 8) return
      this.deck.push(card)
      this.cards.map((listCard) => {
        if (listCard.name === card.name) listCard.inDeck = true
        return listCard
      })
      localStorage.setItem('deck', JSON.stringify(this.deck))
    }
  },
  computed: {
    configureCards() {
      this.cards = this.shuffle(cardsList)
    }
  },
  mounted() {
    let deck = localStorage.getItem('deck')
    if (deck !== null) this.deck = JSON.parse(deck)
    this.configureCards
    this.checkExist
  }
}
</script>
<style>
@font-face {
  font-family: 'Clash';
  src: url('../assets/CR.woff2') format('woff2');
}
body {
  font-family: Clash;
}
.controlls {
  display: block;
  height: 10rem;
  color: rgb(116, 88, 4);
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #50b1fe;
  box-shadow: 15px 10px #3679af;
  margin-top: 2rem;
  border-radius: 20px;
  margin-bottom: 3rem;
}
.button {
  display: inline-block;
  padding: 10px 20px;
  border: none;
  background-color: #f8c471;
  color: #ffffff;
  font-size: 16px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.counter {
  font-size: 3rem;
}
.btn-clash.two {
  width: 250px;
  height: 100px;
  border: none;
  border-radius: 5px;
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  background: none;
  cursor: pointer;
  padding: 12px 10px;
  display: inline-block;
  margin: 15px 30px;
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
