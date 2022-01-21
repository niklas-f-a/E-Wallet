<template>
  <main class="main">
    <h1>ADD A NEW BANK CARD</h1>
    <small>NEW CARD</small>
    <NewCard :info='input' />
    <form @submit.prevent="">
      <label for="card-number">CARD NUMBER</label>
      <input v-model='input.cardNumber' @input="inputCheck" type="text" id="card-number" name="card-number">
      <label for="card-holder">CARDHOLDER NAME</label>
      <input v-model="input.cardHolder" type="text" id="card-holder" name="card-holder">
      <div>
        <span>
          <label for="valid-to">VALID THRU</label><br>
          <input @input="formatValidThru" v-model="input.validThru" type="text" id="valid-to" name="valid-to">
        </span>
        <span> 
          <label for="ccv">CCV</label><br>
          <input @input="maxLengthCcv" v-model="input.ccv" type="text" id="ccv" name="ccv">
        </span>
      </div>
      <label for="vendor">VENDOR</label>
      <select @change="select" v-model="input.vendor" name="vendor" id="vendor">
        <option value="bitcoin-inc">BITCOIN INC</option>
        <option value="ninja-bank">NINJA BANK</option>
        <option value="block-chain-inc">BLOCK CHAIN INC</option>
        <option value="evil-corp">EVIL CORP</option>
      </select>
      <button >ADD CARD</button>
    </form>
  </main>
</template>

<script>
import NewCard from '../components/NewCard'
export default {
  components: {NewCard},
  data(){return {
    input:{
      vendor: '',
      cardNumber: '', 
      cardHolder: '', 
      validThru: '',
      ccv:'',
      img: '',
      color:'',
    }, 
    
  }},
  computed:{
  },
  methods:{
    maxLengthCcv(){
      this.input.ccv = this.input.ccv.substring(0, 3)
    },
    select(){     
      this.input.img = require(`@/assets/${this.input.vendor}.svg`)
      switch(this.input.vendor){
        case "bitcoin-inc": this.input.color = '#FFAE34';break;
        case "ninja-bank": this.input.color = '#222222';break;
        case "block-chain-inc": this.input.color = '#8B58F9';break;
        case "evil-corp": this.input.color = '#F33355';break;
        default: this.input.color = '#D0D0D0'
      }
    },
     inputCheck(){
      if(this.input.cardNumber.length >= 16){
        this.input.cardNumber = this.input.cardNumber.substring(0, 16)
      }
    },
    formatValidThru(){
        if(this.input.validThru.length >= 4){
        this.input.validThru = this.input.validThru.substring(0, 4)
      }
    }
  }
}
</script>

<style lang='scss' scoped>
  h1{
    width: 10rem;
    text-align: center;
  }
  form{
  margin: 3rem auto 1rem auto;
  display: flex;
  flex-direction: column;
  width: 90%;
  input, select{
    margin-bottom: 1rem;
    padding: 1rem;
    border-radius: 8px;
    border: 1px solid black;
  }
  label{
    font-size: 12px;
  }
  div{
    display: flex;
    justify-content: space-between;
    input{
    width: 10rem;
    }
  }
  button{
    font-size: 22px;
    font-weight: bolder;
    padding: 1rem;
    background-color: black;
    color: white;
    border-radius: 8px;
    border: none;
  }
}
 
  
</style>