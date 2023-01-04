<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Pesquisar..."
          v-model="query"
          @keypress="fetchWeather"
        >     
      </div>

      <div 
        class="weather-wrap" 
        v-if="typeof weather.main != 'undefined'"
      >
        <div class="location-box">
          <div class="location">
            <b-icon icon="geo-alt-fill"></b-icon>
            {{ weather.name }}
            <img
             class="flag"
             :src="`https://countryflagsapi.com/png/${weather.sys.country}`"
             crossorigin="anonymus" 
             alt="flag">       
        </div>
        </div>

        <div class="weather-box">
          <div class="weather">
            <img class="nuvem" :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`" alt="clima">
          </div>
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      api_key: '36b833d54ab1752569c9ae7e7f5f2b40',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
    }
  },

  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&lang=pt&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },

    setResults(results){
      console.log(results)
      this.weather = results;
    },
  },

  components: {

  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'montserrat', sans-serif;
  }

  #app {
    background: rgb(2,0,36);
    background: linear-gradient(146deg, rgba(2,0,36,1) 0%, rgba(9,22,121,1) 35%, rgba(0,212,255,1) 100%);
    background-size: cover;
    background-position: bottom;
    transition: .4s;
  }

  main {
    min-height: 100vh;
    padding: 25px;
  
  }

  .search-box {
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;

    color: #FFF;
    font-size: 20px;

    appearance: none;
    border: none;
    outline: none;
    background: none;

    box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.5);
    border-radius: 16px;
    transition: .4s;
  }

  .search-box .search-bar::placeholder {
    color: #FFF;
  }

  .search-box .search-bar:focus {
    box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.75);
  }

  .location-box .location {
    color: #FFF;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  }

  .location-box .flag {
    height: 5vh;
    box-shadow: 10px 10px 51px -5px rgba(0,0,0,0.41);
  }

  .nuvem {
    height: 15vh;
  }

  .weather-box {
    text-align: center;
  }

  .weather-box .temp {
    display: inline-block;
    padding: 10px 25px;
    color: #FFF;
    font-size: 102px;
    font-weight: 900;

    text-shadow:3px 6px rgba(0, 0, 0 , 0.25);
    background-color: rgba(255,255,255,0.25);
    border-radius: 10px;
    margin: 30px 0px;

    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }

  .weather-box .weather {
    color: #FFF;
    font-size: 30px;
    font-weight: 500;
    text-shadow: 2px 2px 6px rgba(0,0,0,0.57);
  }
</style>
