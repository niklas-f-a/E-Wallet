<template>
  <article class="credit-card" 
    :class="[{active: card.active}, {bitcoin: card.vendor == 'bitcoin-inc', blockchain: card.vendor == 'block-chain-inc', 
      ninja: card.vendor == 'ninja-bank', evil: card.vendor == 'evil-corp'}]"
    @click="activate"
  >
    <div v-if="removeOption" class="check-box">
      <input type="checkbox"  
        :checked='card.remove'
        @click.stop="checkThis"       
      >
    </div>
    <span class="chip-img">
      <img src="../assets/wifi_dark.svg" alt="">
      <img src="../assets/chip.svg" alt="">
    </span>
    <img :src="card.imgFile" alt="">
    <h3 v-if="card">{{cardNumberWithSpaces}}</h3>
    <span class="name">
      <p>CardHolder Name</p>
      <h5>{{card.cardHolder.toUpperCase()}}</h5>
    </span>
    <span class="valid">
      <p>Valid thru</p>
      <p>{{card.expireMonth}}/{{card.expireYear}}</p>
    </span>
  </article>
</template>

<script>
export default {
  props: ['card', 'removeOption'],
  computed:{
    cardNumberWithSpaces(){
      return `${this.card.cardNumber.substring(0, 4)} 
        ${this.card.cardNumber.substring(4, 8)} 
        ${this.card.cardNumber.substring(8, 12)} 
        ${this.card.cardNumber.substring(12, 16)}`
    }
  },
  methods:{
    checkThis(){
      this.$emit('check', this.card)
    },
    activate(){
      this.$emit('activate', this.card)
    }
  }
}
</script>
<style lang='scss'>
.check-box{
  border-radius: 35%;
  width: 25px;
  height: 25px;
  background-color: rgba(207, 82, 82, 0.411);
  position: absolute;
  left: -28px;
  top: 10px;
  display: grid;
  place-items: center;
}
.evil{
  background-color: #F33355;
}
.ninja{
  background-color: #222222;
}
.blockchain {
  background-color: #8B58F9;
}
.bitcoin{
  background-color: #FFAE34;
}
.bitcoin > span > h5,.bitcoin > span > p, .bitcoin > h3{
  color:#000000;  
    h3, p, h5 {
      text-shadow: .5px .5px 0px rgba(254, 254, 254, .24) inset;
    }  
  .valid  p{
    text-shadow: -.5px -.5px 0px rgba(255, 255, 255, .25);
    text-shadow: .5px .5px 0px rgba(255, 255, 255, .5);
    }
  }
.credit-card{
  position: relative;
  height: 10rem;
  width: 17rem;
  border-radius: 8px;
  padding: .5rem 1rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 3rem 1fr 4rem 1fr 1fr;
  background-image: linear-gradient(to top right, rgba(0,0,0,0),rgba(0, 0 , 0 , .16) );
  box-shadow: 0px 0px 8px 0px rgba(0,0,0,0.25);
  -webkit-box-shadow: 0px 0px 8px 0px rgba(0,0,0,0.25);
  -moz-box-shadow: 0px 0px 8px 0px rgba(0,0,0,0.25);
  :hover{
    cursor: pointer;
  }
  .chip-img{
    grid-row: 1 / span 2;
    grid-column: 1 / 2;
    display: flex;
    flex-direction: column;
  }
  img{
    grid-row: 1 / 2;
    grid-column: 4 / 5;
    justify-self: end;
    width: 2rem;
  }
  h3{
    font-weight: 400;
    grid-row: 3 / 4;
    grid-column: 1 / 5;
    align-self: center;
    font-size: 21px;
    letter-spacing: 1.5px;
  }
  .name{
    display: flex;
    flex-direction: column;
    grid-row: 4 / 6;
    grid-column: 1 / 4;
    justify-content: flex-start;
    p{
      font-size: 10px;
    }
    h5{
     font-weight: 300;
    }
  }
  .valid {
    display: flex;
    flex-direction: column;
    grid-row: 4 / 6;
    grid-column: 4 / 6;
    align-items: end;
     p:first-child{
      font-size: 10px;
    }p:last-of-type{
      font-weight: 300;
      font-size: 16px;
    }
  }
  h3, span > p, span > h5{
    text-shadow: -.5px -.5px 0px rgba(255, 255, 255, .25);
    text-shadow: .5px .5px 0px rgba(255, 255, 255, .5);
  }
 
}
</style>