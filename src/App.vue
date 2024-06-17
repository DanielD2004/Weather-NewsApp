<script setup>
  import Weather from './components/Weather.vue'
  import News from './components/News.vue'
</script>

<template lang="">

  <div id="container">
    <div id="weather-container">
      <Weather/>
    </div>

    <div id="news-container">
      <News/>
    </div>
  </div>  
</template>

<style scoped>

  body{
    margin: 0px;
  }

  #container{
    display:flex;
    width:100vw;
    height:100vh;
  }
  
</style>