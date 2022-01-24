<template>
  <main class="main">
    <h1>ADD A NEW BANK CARD</h1>
    <small>NEW CARD</small>
    <NewCard :info='input' /> 
    <form @submit.prevent="validateInput">
      <label for="card-number">CARD NUMBER</label>
      <input :class="{errorborder: error.cardNr}" v-model='input.cardNumber' @input="inputCheck" placeholder="XXXX XXXX XXXX XXXX" type="number" id="card-number" name="card-number" ref="focusMe">
      <small :class="{error: error.cardNr}">{{error.cardNr}}</small>
      <label for="card-holder">CARDHOLDER NAME</label>
      <input :class="{errorborder: error.name}" @input="validCharacter" v-model="input.cardHolder" placeholder="Firstname Lastname" type="text" id="card-holder" name="card-holder">
      <small :class="{error: error.name}">{{error.name}}</small>
      <div>
        <span>
          <label for="valid-to">VALID THRU</label><br>
          <input :class="{errorborder: error.monthAndYear}" @change="getDates" type="month" min="2022-01" max="2027-12" id="valid-to" name="valid-to"><br>
          <small :class="{error: error.monthAndYear}">{{error.monthAndYear}}</small>
        </span>
        <span> 
          <label for="ccv">CCV</label><br>
          <input :class="{errorborder: error.ccv}" @input="maxLengthCcv" v-model="input.ccv" type="number" id="ccv" name="ccv"><br>
          <small :class="{error: error.ccv}">{{error.ccv}}</small>
        </span>
      </div>
      <label for="vendor">VENDOR</label>
      <select :class="{errorborder: error.vendor}" @change="select" v-model="input.vendor" name="vendor" id="vendor">
        <option value="bitcoin-inc">BITCOIN INC</option>
        <option value="ninja-bank">NINJA BANK</option>
        <option value="block-chain-inc">BLOCK CHAIN INC</option>
        <option value="evil-corp">EVIL CORP</option>
      </select>
      <small :class="{error: error.vendor}">{{error.vendor}}</small>
      <button>ADD CARD</button>
    </form>
    <div class="uniqueModal" v-if="!uniqueNr">hahahhahaha</div>
  </main>
</template>

<script>

import NewCard from '../components/NewCard'
export default {
  components: {NewCard},
  props: ['cards'],
  mounted(){
      document.querySelector('input:first-of-type').focus()
      console.log(this.cards);
  },
  data(){return {
    input:{
      expireMonth: '', 
      expireYear: '', 
      vendor: '',
      cardNumber: '', 
      cardHolder: '', 
      ccv:'',
      imgFile: '',
      color:'',
    }, 
    noNumbers: false,
    nameValid: false,
    monthAndYearValid: false,
    ccvValid: false,
    vendorValid: false,
    cardNrValid: false,
    uniqueNr: true,
    error: {
      name:'',
      monthAndYear:'',
      ccv:'',
      vendor:'',
      cardNr:''
    }
  }},
  methods:{
    validCharacter(e){
      if(e.target.value < 1){
        this.error.name = ''
      }
      if(e.target.value.match(/^[A-Za-z\s]+$/)){
        this.noNumbers = true
        this.error.name = ''      
      }else {        
        this.error.name = 'NO NUMBERS'
        this.noNumbers = false
      }
     
    },
    validateInput(){
      //console.log(this.input.cardNumber == this.cards[0].cardNumber);
      const exists = this.cards.find(c => c.cardNumber == this.input.cardNumber)
      console.log(!exists);
      if(exists){
        this.uniqueNr = false
      }else{ 
        this.uniqueNr = true
      }
      if(!/\s/.test(this.input.cardHolder)){
        this.error.name = 'MUST HAVE FIRST AND LAST NAME' }
        else{
        this.nameValid = true
      }
      if(!this.monthAndYearValid){
        this.error.monthAndYear = 'NEEDED'
      }
      if(!this.vendorValid){
        this.error.vendor = 'NEED TO PICK A VENDOR'
      }
      if(!this.cardNrValid){
        this.error.cardNr = 'CARD NUMBER MUST BE 16 DIGITS'
      }
      if(!this.ccvValid){
        this.error.ccv = 'NEEDED'
      }
      if(this.nameValid && this.monthAndYearValid && this.vendorValid && this.uniqueNr
        && this.cardNrValid && this.ccvValid && this.noNumbers){
          this.$emit('cardInfo', {...this.input})
      } 
    },      
    getDates(e){
      const [year, month] = e.target.value.split('-')
      this.input.expireYear = year.substring(2, 4)
      this.input.expireMonth = month
      this.monthAndYearValid = true
    },
    maxLengthCcv(){
      this.input.ccv = this.input.ccv.substring(0, 3)
      if(this.input.ccv.length > 2){this.ccvValid = true}
        else{this.ccvValid = false}
    },
    select(){     
      this.input.imgFile = require(`@/assets/${this.input.vendor}.svg`)
      this.vendorValid = true
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
        this.cardNrValid = true
      }else{
        this.cardNrValid = false
      }
    },
  }
}

</script>

<style lang='scss' scoped>
.error{
  color: red;
}
.errorborder{
  border: 1px solid red;
}
  h1  {
    width: 11rem;
    text-align: center;
    margin-bottom: 1rem;
  }
  
  form{
  margin: 3rem auto 1rem auto;
  display: flex;
  flex-direction: column;
  width: 90%;
  input, select{
    padding: 1rem;
    border-radius: 8px;
    border: 1px solid black;
  }
  small{
    margin-bottom: 1rem;
    font-size: 10px;
  }
  label{
    font-size: 12px;
  }
  div{
    display: flex;
    justify-content: space-between;
    input{
    width: 6rem;
    }
    input:first-of-type{
      height: .7rem;
      font-size: 10px;
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
    cursor: pointer;
    &:hover{
      background-color: white;
      color: #000000;
      border: 1px solid #000000;
    }
  }
}
 
  
</style>