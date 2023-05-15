<template>
  <div class="parent">
    <div v-for="card in cards" class="main">
      <img :src="card.imgUrl" :alt="'Image of ' + card.name" />
      <h1>{{ card.name }}</h1>
      <p>Rarity: {{ card.rarity }}</p>
      <p>Elixir: {{ card.elixirCost }}</p>
      <button class="btn-clash one" v-if="card.inDeck" disabled>
        <div class="overlay"></div>
        <div class="overlay"></div>
        <div class="overlay"></div>
        <span>Card In Deck</span>
      </button>
      <button class="btn-clash one" v-else @click="(event) => $emit('toDeck', card)">
        <div class="overlay"></div>
        <div class="overlay"></div>
        <div class="overlay"></div>
        <span>Add To Deck</span>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  emits: ['toDeck'],
  props: {
    cards: {
      type: Array,
      required: true
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
  font-family: 'Clash';
}

.parent {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
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

</style>
