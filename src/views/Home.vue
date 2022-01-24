<template>
  <main class="main">
    <h1>E-Wallet</h1>
    <small>ACTIVE CARD</small>
    <CreditCard v-if="active.vendor" :card='active'/>
    <h1 v-else>no active</h1>
    <!-- <h1 v-if="active.vendor && !cards[0]">you have no cards here</h1>   -->
    <div class="cards"
      :style="{height: cards.length * 2.5 + 10 + 'rem'}"
    >
      <!-- <h1 v-else-if="!active.card && !cards[0]">no cards</h1>       -->
      <CreditCard v-for="(card, index) in cards"
        class="other-cards"
        @activate="$emit('activateCard', card)"
        :key="card.cardNumber"
        :card='card'
        :style="{top: index * 2.5 +'rem'}"
      />
    </div>
    <button @click="$emit('newCard')" >ADD A NEW CARD</button>
  </main>
</template>

<script>
import CreditCard from '../components/CreditCard'
export default {
  components: { CreditCard },
  props: ['cards', 'active'],
}
</script>

<style lang='scss' scoped>
small{
  margin-bottom: .5rem;
  font-size: 10px;
}
h1{
  margin: 1.5rem auto 1.5rem auto;
  font-weight: bold;
}
p{
  margin-bottom: .5rem;
  font-size: .7rem;
}
.active{
  margin-bottom: 1.5rem;
}
.other-cards{
  position: absolute;
}
.cards{
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 20rem;   
  position: relative;
  :hover{
    cursor: pointer;
  }
}
button{
  font-size: 22px;
  font-weight: bolder;
  padding: 1rem;
  background-color: white;
  color: black;
  border-radius: 8px;
  border: 1px solid black;
  width: 95%;
  margin-bottom: 1rem;
}
</style>