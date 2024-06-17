<template>
    <div id="main">
      <input id="searchBar" placeholder="Enter a location" @keypress="getWeather" v-model="search" type="text">
      <div id="weatherInfo" v-if="typeof weather.main !='undefined'" >
        <div id="location">{{ (weather.name).toUpperCase() }}</div>
        <div id="day"></div>
        <div id="temp" :class="weather.main.temp > 15 ? 'hot' : 'cold'">{{ Math.round(weather.main.temp) + '°' }}</div>
        <div id="weather-style">{{ (weather.weather[0].description).toUpperCase() }}</div>
      </div>
    </div>
    
  </template>
  
  <script>
    export default{
      name: 'app',
      data(){
        return{
          search: "",
          apiKey: "0f833f560467ab8827b2d6d12fb27107",
          url: "https://api.openweathermap.org/data/2.5/",
          weather: {}
        }
      },
      methods:{
        getWeather (press) {
          if (press.key == "Enter") {
            fetch(`${this.url}weather?q=${this.search}&units=metric&APPID=${this.apiKey}`)
            .then(data => {
              return data.json();
            }).then(this.setResponse);
            this.search = ""
          }
        },
        setResponse(response){
          this.weather = response
        }
      }
    }
  </script>
  
  
  <style scoped>
  
    #main{
      font-family: "Comic Sans MS", "Comic Sans", cursive;
      background-image: linear-gradient(blue, red);
      background-repeat: no-repeat;
      background-size:cover;
      height:100vh;
      width:25vw;
      padding:30px;
      text-align: center;
      white-space:nowrap;
      overflow: hidden;
      font-weight:bold;
      margin:-8px;
    }
  
    #location{
      color:white;
      font-size:75px;
    }
  
    #temp{
      width:200px;
      height:100px;
      background-image: linear-gradient(rgba(0,0,0,0.2), rgba(255,255,255,0.3));
      font-size:60px;
      margin:auto;
      border-radius:50px;
      padding-left:15px;
    }
    .hot{
      color:red;
    }
  
    .cold{
      color:white;
    }
  
    #searchBar{
      margin-top:75px;
      height:50px;
      width:25vw;
      border-radius:50px 0 50px 0;
      padding:10px;
    }

    #weather-style{
      font-size: 50px;
      margin-top:30px;
      color:white;
    }
  </style>
  