<template>
  <div id="e-wallet">
    <Home v-if="currentView === 'home'" />
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
  data(){return {
    currentView: 'home'

  }}
}
</script>

<style lang="scss">

</style>
