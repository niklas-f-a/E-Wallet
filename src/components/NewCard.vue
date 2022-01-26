<template>
  <article class="new-card" 
    :class="{bitcoin: info.vendor == 'bitcoin-inc', blockchain: info.vendor == 'block-chain-inc', 
      ninja: info.vendor == 'ninja-bank', evil: info.vendor == 'evil-corp'}"
  >
    <span class="chip-img">
      <img src="@/assets/wifi_white.svg">
      <img src="@/assets/chip.svg" alt="">
    </span>
    <img v-if="info.imgFile" alt=""
      :src="info.imgFile"
    >
    <h3>
      {{cardNr}} 
    </h3>
    <span class="name">
      <p>Cardholder Name </p>
      <h4>{{info.cardHolder.toUpperCase()}}</h4>
    </span>
    <span class="valid">
      <p>Valid thru</p>
      <p v-if="!info.expireMonth">MM/YY</p>
      <p v-else>{{info.expireMonth}}/{{info.expireYear}}</p>
    </span>
  </article>
</template>

<script>
export default {
  props: {
    info: Object,
  },
  computed:{
    cardNr(){
      return `${this.info.cardNumber.substring(0, 4)} 
        ${this.info.cardNumber.substring(4, 8)} 
        ${this.info.cardNumber.substring(8, 12)} 
        ${this.info.cardNumber.substring(12, 16)}`
    }
  }

}
</script>

<style lang='scss' scoped>
.bitcoin > span > h4,.bitcoin > span > p, .bitcoin > h3{
  color:#000000; 
  h3, p, h4 {
      text-shadow: .5px .5px 0px rgba(254, 254, 254, .24) inset;
  } 
}
.new-card.bitcoin{
  background-color: #FFAE34;
}
.new-card.ninja{
  background-color: #222222;
}
.new-card.blockchain{
  background-color: #8B58F9;
}
.new-card.evil{
  background-color: #F33355;
}
.new-card{
  background-color: #D0D0D0;
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
    align-items: start;
    justify-content: flex-start;
    p{
      font-size: 12px;
      
    }
    h4{
      font-family: 'PT Mono', monospace;
      font-size: 16px;
      font-weight: 300;
      
    }
  }
  .valid {
    display: flex;
    flex-direction: column;
    grid-row: 4 / 6;
    grid-column: 4 / 6;
    align-items: end;
    justify-content: flex-start;
    .valid  p{
    text-shadow: -.5px -.5px 0px rgba(255, 255, 255, .25);
    text-shadow: .5px .5px 0px rgba(255, 255, 255, .5);
    }
     p:first-child{
      font-size: 10px;
     
      
    }p:last-of-type{
      font-family: 'PT Mono', monospace;
      font-weight: 300;     
    }
  }
  h3, span > p, span > h4{
    text-shadow: -.5px -.5px 0px rgba(255, 255, 255, .25);
    text-shadow: .5px .5px 0px rgba(255, 255, 255, .5);
  }
 
}
</style>