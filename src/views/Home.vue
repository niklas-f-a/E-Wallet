<template>
  <main class="main">
    <h1>E-Wallet</h1>
    <p>ACTIVE CARD</p>
    <div class="cards">
      <CreditCard v-if="active.vendor" :card='active'/>
      <h1 v-else>no active</h1>
      <h1 v-if="active.vendor && !cards[0]">you have no cards here</h1>
      <!-- <h1 v-else-if="!active.card && !cards[0]">no cards</h1>       -->
      <CreditCard v-for="card in cards"
        @activate="$emit('activateCard', card)"
        :key="card.cardNumber"
        :card='card'
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
h1{
  margin: 1.5rem auto 1.5rem auto;
  font-weight: bold;
}
p{
  margin-bottom: .5rem;
  font-size: .7rem;
}
.active{
  margin-bottom: 3rem;
}
.cards{
  width:100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  min-height: 30rem;
   
}
button{
  font-size: 22px;
  font-weight: bolder;
  padding: 1rem;
  background-color: white;
  color: black;
  border-radius: 8px;
  border: 1px solid black;
  width: 90%;
  margin: 2rem auto 1rem auto;
}
</style>