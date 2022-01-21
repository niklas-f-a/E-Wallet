<template>
  <main class="main">
    <h1>E-Wallet</h1>
    <small>ACTIVE CARD</small>
    <div class="cards">
      <CreditCard :card='active' />
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
  margin: 1rem auto 3rem auto;
}
small{
  margin-bottom: .5rem;
}
.active{

  top: 0;
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