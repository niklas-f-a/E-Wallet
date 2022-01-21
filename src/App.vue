<template>
  <div id="e-wallet">
    <Home v-if="currentView === 'home'" 
      :cards='stack'
      :active='activeCard'
      @activateCard='activate'
      @newCard='newCardPage'
    />
    <AddCard v-else-if="currentView === 'addcard'" />
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
  methods: {
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
    }
  },
  computed: {
    stack(){
      return this.vendorCards.filter(card => card.active === false)
    }
  },
  data(){return {
    currentView: 'addcard',
    activeCard: {
      vendor: 'bitcoin-inc',
      cardNumber: '1234 4567 8912 3456', 
      cardholder: 'eldar bin', 
      expireMonth: 12, 
      expireYear: 31, 
      CCV:123,
      imgFile: require('@/assets/bitcoin-inc.svg'), 
      color: '#FFAE34',
      active: true
    },
    vendorCards: [{
      vendor: 'bitcoin-inc',
      cardNumber: '1234 4567 8912 3456', 
      cardholder: 'eldar bin', 
      expireMonth: 12, 
      expireYear: 31, 
      CCV:123,
      imgFile: require('@/assets/bitcoin-inc.svg'), 
      color: '#FFAE34',
      active: true
    }, 
    {
      vendor: 'ninja-bank',
      cardNumber: '9876 5432 1987 6543', 
      cardholder: 'bingo lotto', 
      expireMonth: 5, 
      expireYear: 25, 
      CCV:445,
      imgFile: require('@/assets/ninja-bank.svg'),
      color: '#222222',
      active: false
    },
    {
      vendor: 'block-chain-inc',
      cardNumber: '6543 1234 5687 7895', 
      cardholder: 'lingon bär', 
      expireMonth: 2, 
      expireYear: 23, 
      CCV:454,
      imgFile: require('@/assets/block-chain-inc.svg'),
      color: '#8B58F9',
      active: false
    },
    {
      vendor: 'evil-corp',
      cardNumber: '7854 4563 3215 5468', 
      cardholder: 'skalman skal', 
      expireMonth: 4, 
      expireYear: 65, 
      CCV:134,
      imgFile: require('@/assets/evil-corp.svg'),
      color: '#F33355',
      active: false
    }]
  }}
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=PT+Mono&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@300&display=swap");
$textFont: 'Source Sans Pro', sans-serif;
$numberFont: 'PT Mono', monospace;
$red: f33355;
html, body, h1, h2, h3, h4, p {
  margin: 0;
  padding: 0;
}
h1, h2, h4, p, button{
  font-family: $textFont;
}
h3{
  font-family: $numberFont;
}
body{
  background-color: gray;
}
.main{
  width: 100vw;
  padding: 1rem;
  background-color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 2px;
}
</style>
