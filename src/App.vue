<template>
  <div id="e-wallet">
    <Home v-if="currentView === 'home'" 
      :cards='stack'
      :active='activeCard'
      @activateCard='activate'
      @newCard='newCardPage'
    />
    <AddCard v-else-if="currentView === 'addcard'" 
      @cardInfo='collect'
      :cards="vendorCards"
    />
  </div>
</template>

<script>
import * as Views from './views' 

export default {
  name: 'E-wallet',
  components: {
    Home: Views.Home, 
    AddCard: Views.AddCard
  },
  created(){
    const cards = localStorage.getItem('cards')
    if(cards){
      this.vendorCards = [...JSON.parse(cards)]
      this.vendorCards.forEach(card => card.imgFile = require(`@/assets/${card.vendor}.svg`))
      this.activeCard = this.vendorCards.find(c => c.active === true)
      console.log(this.vendorCards);
    }
  },
  methods: {
    collect(card){
      
      card.active = false
      this.vendorCards.push(card)
      localStorage.setItem('cards', JSON.stringify(this.vendorCards))
      this.currentView = 'home'
    },
    newCardPage(){
      this.currentView = 'addcard'
    },
    expiration(card){
    return `${card.expireMonth}/${card.expireYear}`
    },
    activate(card){
      this.vendorCards.forEach(c => c.active = false)
      card.active = true
      this.activeCard = card
      localStorage.setItem('cards', JSON.stringify(this.vendorCards))
    }
  },
  computed: {
    stack(){
        return this.vendorCards.filter(card => card.active === false)
    }, 
  },
  data(){return {
    currentView: 'home',
    activeCard: {},
    vendorCards: [], 
  }}
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=PT+Mono&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@300&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@700&display=swap");
$textFont: 'Source Sans Pro', sans-serif;
$cardFont: 'PT Mono', monospace;

html, body, h1, h2, h3, h4, p, h5 {
  margin: 0;
  padding: 0;
}
h1, h2, button{
  font-family: $textFont;
}
h4, h3, p, h5{
  font-family: $cardFont;
  color: #FFFFFF;
}
body{
  background-color: rgb(190, 190, 190);
  display: flex;
  justify-content: center;
}
.main{
  margin-top: 2rem;
  width: 23rem;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 2px;
}
</style>
