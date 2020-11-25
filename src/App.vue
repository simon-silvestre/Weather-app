<template>
  <div id="app">
    <div class="smartphone-container">
      <div class="smartphone-container__meteo">
        <div class="meteo__actuelle">
          <p>{{ weather.name }}, {{ weather.sys.country }}</p>
          <p id="meteo__degrés">{{ Math.round(weather.main.temp) }}°</p>
          <p>{{ weather.weather[0].main }}</p>
        </div>
        <div class="meteo__future">
          <div class="meteo__future__jour">
            <p>{{ fiveWeather.list[2].dt_txt | formatDate }}</p>
              <div class="jour__degre">
                <p>{{ Math.round(fiveWeather.list[2].main.temp) }}°</p>
                <img :src="'http://openweathermap.org/img/wn/' + fiveWeather.list[2].weather[0].icon + '.png'">
                <!-- fiveWeather.list[2].weather[0].icon  -->
              </div>
          </div>

          <div class="meteo__future__jour">
            <p>{{ fiveWeather.list[10].dt_txt | formatDate }}</p>
              <div class="jour__degre">
                <p>{{ Math.round(fiveWeather.list[10].main.temp) }}°</p>
                <img :src="'http://openweathermap.org/img/wn/' + fiveWeather.list[10].weather[0].icon + '.png'">
            </div>
          </div>

          <div class="meteo__future__jour">
            <p>{{ fiveWeather.list[18].dt_txt | formatDate }}</p>
              <div class="jour__degre">
                <p>{{ Math.round(fiveWeather.list[18].main.temp) }}°</p>
                <img :src="'http://openweathermap.org/img/wn/' + fiveWeather.list[18].weather[0].icon + '.png'">
            </div>
          </div> 

          <div class="meteo__future__jour">
            <p>{{ fiveWeather.list[26].dt_txt | formatDate }}</p>
              <div class="jour__degre">
                <p>{{ Math.round(fiveWeather.list[26].main.temp) }}°</p>
                <img :src="'http://openweathermap.org/img/wn/' + fiveWeather.list[26].weather[0].icon + '.png'">
            </div>
          </div>

          <div class="meteo__future__jour">
            <p>{{ fiveWeather.list[34].dt_txt | formatDate }}</p>
            <div class="jour__degre">
              <p>{{ Math.round(fiveWeather.list[34].main.temp) }}°</p>
              <img :src="'http://openweathermap.org/img/wn/' + fiveWeather.list[34].weather[0].icon + '.png'">
            </div>
          </div>

        </div>
      </div>

      <div class="smartphone-container__location">
        <form @submit.prevent="getWeather">
          <input type="text" v-model="location" placeholder="changer de ville">
        </form>
     </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import moment from 'moment'
  
Vue.config.productionTip = false
Vue.filter('formatDate', function(value) {
  if (value) {
    return moment(String(value)).format('dddd')
  }
});

export default {
  name: 'App',
  data() {
      return {
          location: 'Paris',
          api_key: '772f1145fd85515774a60b7277b22c94',
          api_url: 'https://api.openweathermap.org/data/2.5/',
          weather: {},
          fiveWeather: {},
      }
  },
  created() {
    this.getWeather()
  },
  methods: {
    getWeather() {
      fetch(`${this.api_url}weather?q=${this.location}&units=metric&appid=${this.api_key}`)
        .then((response) => response.json())
          .then(data => this.weather = data);
          this.getFiveDaysWeather()
          this.location = ""
    },
    getFiveDaysWeather() {
      fetch(`${this.api_url}forecast?q=${this.location}&units=metric&appid=${this.api_key}`)
        .then((response) => response.json())
          .then(data => this.fiveWeather = data);
    },
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }
  #app {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-image: linear-gradient(62deg, rgb(128, 169, 185) 0%, rgb(94, 146, 180) 100%);


    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  .smartphone-container {
    width: 400px;
    height: 700px;

   box-shadow: 0px 3px 24px -2px rgb(100, 100, 109);
  }

  .smartphone-container__meteo {
    width: 100%;
    height: 595px;
  }
  .meteo__actuelle {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    height: 45%;
    background-color: #0093E9;
    background-image: linear-gradient(160deg, #0093E9 0%, #80D0C7 100%);
  }
  .meteo__actuelle p:nth-child(1) {
    text-transform: uppercase;
  }
  .meteo__actuelle p:nth-child(3) {
    margin: 3px 5px 0 0;
    font-size: 16px;
  }
  .meteo__actuelle p {
    text-align: center;

    color: #fff;
    font-weight: 500;
    font-size: 14px;
  }
  #meteo__degrés {
    height: 58px;
    font-size: 55px;
    font-weight: 900;
    margin-left: 12px;
  }
  .meteo__future {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    height: 55%;
    background-color: #fff;
  }
  .meteo__future__jour:nth-child(1) {
    margin-top: 0;
  }
  .meteo__future__jour {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 55%;
    margin-top: 10px;

    color: #868f9e;
    font-weight: 500;
    font-size: 17px;
  }
  .jour__degre  {
    display: flex;
    align-items: center;
    font-weight: 900;
  }
  .jour__degre img {
    width: 45px;
    margin-left: 15px;
  }

  .smartphone-container__location {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 100%;
    height: 105px;
    background-color: #868f9e;
  }
  .smartphone-container__location form {
    width: 70%;
    height: 35px;
  }
  .smartphone-container__location input {
    width: 100%;
    height: 100%;
    text-align: center;

    background-color: rgba(255, 255, 255, 0.699);
    border: none;
    border-radius: 10px 0 10px 0;
    outline: none;

    color: #868f9e;
    font-weight: 600;
  }

  @media screen and (max-width: 500px) {
    .smartphone-container {
      width: 100%;
      height: 100vh;
    }
    .smartphone-container__meteo {
      height: 85%;
    }
    .smartphone-container__location {
      height: 15%;
    }
    .meteo__actuelle {
      height: 40%;
    }
    .meteo__future {
      height: 60%;
    }
    .smartphone-container__location input {
      font-size: 16px
    }
  }
   @media screen and (max-width: 320px) {
    .meteo__future__jour {
      font-size: 14px;
    }
    .jour__degre img {
      width: 40px;
    }
   }
</style>
