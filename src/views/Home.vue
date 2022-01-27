<template>
  <main class="main">
    <h1>E-Wallet</h1>
    <small>ACTIVE CARD</small>
    <CreditCard
      v-if="active.active"
      :card='active' 
      @activate="$emit('activateCard', active)"
    />
    <h1 v-else>no active</h1>
    <div class="cards"
      :style="{height: cards.length * 2.5 + 10 + 'rem'}"
      
    >
      <CreditCard v-for="card in cards"
        @activate="$emit('activateCard', card)"
        :key="card.cardNumber"
        :card='card'
        :removeOption='option'
        @check="$emit('checkIt', card)"
      />
    </div>
    <span class="btn-controler">
      <button @click="$emit('remove')" v-if="option" class="remove">REMOVE</button>
      <button v-if="!option" class="removebtn" @click="$emit('toggleRemove')">REMOVE CARD</button>
      <button v-else class="removebtn cancel" @click="$emit('toggleRemove')">CANCEL</button>
    </span>
    <button class="addbtn" @click="$emit('newCard')" >ADD A NEW CARD</button>
  </main>
</template>

<script>
import CreditCard from '../components/CreditCard'
export default {
  components: { CreditCard },
  props: ['cards', 'active', 'option'],
}
</script>

<style lang='scss' scoped>
.btn-controler{
  width: 80%;
  display: flex;
  justify-content: flex-end;
  .removebtn, .remove{
    background-color: white;
    margin-bottom: .5rem;
    margin-left: 1rem;
    font-weight: 600;
    border-radius: 8px;
    &:hover{
      cursor: pointer;
      background-color: red;
      color: white;
    }
  }
}
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
.cards{
  display: grid;
  grid-auto-rows: 2.5rem;
  :hover{
    cursor: pointer;
  }
}

.addbtn{
  font-size: 22px;
  font-weight: bolder;
  padding: 1rem;
  background-color: white;
  color: black;
  border-radius: 8px;
  border: 1px solid black;
  width: 19rem;
  margin-bottom: 1rem;
  cursor: pointer;
  &:hover{
    background-color: #000000;
    color: white;
  }
  
}
</style>