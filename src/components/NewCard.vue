<template>
  <article class="new-card" 
  >
    <span class="chip-img">
    <img src="@/assets/wifi_dark.svg" alt="">
    <img src="@/assets/chip.svg" alt="">
    </span>
    <img :src='info.img' alt="">
    <h3>{{info.cardNumber}}</h3>
    <span class="name">
      <p>Cardholder Name </p>
      <h4>{{info.cardHolder}}</h4>
    </span>
    <span class="valid">
      <p>Valid thru</p>
      <p>{{info.validThru}}</p>
    </span>
  </article>
</template>

<script>
export default {
  props: {info: Object}
}
</script>

<style lang='scss' scoped>
.new-card{
  background-color: #D0D0D0;
  height: 10rem;
  width: 80%;
  border-radius: 8px;
  padding: .5rem 1rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 1fr 1fr 3rem 1fr 1fr;
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
    color: white;
    letter-spacing: .5px;
  }
  .name{
    display: flex;
    flex-direction: column;
    grid-row: 4 / 6;
    grid-column: 1 / 4;
    align-items: start;
    justify-content: center;
    color: white;
    p{
      font-size: 12px;
    }
    h4{
      font-family: 'PT Mono', monospace;
      font-size: 16px;
    }
  }
  .valid {
    display: flex;
    flex-direction: column;
    grid-row: 4 / 6;
    grid-column: 4 / 6;
    align-items: end;
    justify-content: center;
    color: white;
     p:first-child{
      font-size: 12px;
    }p:last-of-type{
      font-family: 'PT Mono', monospace;
      font-weight: 300;
    }
  }
 
}
</style>