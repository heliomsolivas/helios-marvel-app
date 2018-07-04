<template>
  <div id="app">
    <Header></Header>
     <main>
      <CharacterCard></CharacterCard>
   </main>
  </div>
</template>

<script>
import Header from './components/Header'
import CharacterCard from './components/CharacterCard'

export default {
  name: 'App',
  components: {
    Header,
    CharacterCard
  },
}
</script>

<style>
  #app{
    height:100%;
    background-color: #f1f1f1;
  }
</style>
