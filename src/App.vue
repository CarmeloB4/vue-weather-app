<template>
<div id="app">
  <main>
    <div class="search-box">
      <input type="text" class="search-bar" placeholder="Search city" v-model="query" @keypress="featchWeather">
    </div>

    <div id="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
      </div>

    <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
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
      api_key: '9b45c4a0df186c4b12edf4a073f2cc3f',
      url_base: 'https://api.openweathermap.org/data/2.5',
      query: '',
      weather: {}
    }
  },
  methods: {
   featchWeather(e) {
     if (e.key == "Enter") {
       fetch(`${this.url_base}/weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResult);
     }
   },
   setResult (results) {
     this.weather = results;
   }
  }
}
</script>

<style>
* {
  margin:0;
  padding:0;
  box-sizing: border-box;
}

body {
 font-family: 'montserrat', sans-serif;
}

#app {
 background-color: royalblue;
 background-size: cover;
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
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background-color: whitesmoke;
  border-radius: 0px 16px 0px 16px;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
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
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
