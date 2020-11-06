<template>
  <div id="app">
    <div class="smartphone-container">
      <div class="smartphone-container__meteo">
        <div class="meteo__actuelle">
          <p v-if="location != ''">{{ location }}</p>
          <p v-else>Paris, France</p>
          <p id="meteo__degrés">23°</p>
          <p>cloudy</p>
        </div>
        <div class="meteo__future">
          <div class="meteo__future__jour">
            <p>Lundi</p>
              <div class="jour__degre">
                <p>38°</p>
              </div>
          </div>

          <div class="meteo__future__jour">
            <p>Mardi</p>
              <div class="jour__degre">
                <p>38°</p>
            </div>
          </div>

          <div class="meteo__future__jour">
            <p>Mercredi</p>
              <div class="jour__degre">
                <p>38°</p>
            </div>
          </div> 

          <div class="meteo__future__jour">
            <p>Jeudi</p>
              <div class="jour__degre">
                <p>38°</p>
            </div>
          </div>

          <div class="meteo__future__jour">
            <p>Vendredi</p>
            <div class="jour__degre">
              <p>38°</p>
            </div>
          </div>

        </div>
      </div>

      <div class="smartphone-container__location">
        <form @submit.prevent="changeLocation">
          <input type="text" v-model="location" placeholder="changer de ville">
        </form>
     </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
      return {
          location: '',

      }
  },
  methods: {
      changeLocation() {
          console.log(this.location)
          this.location = "";
      }
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
    width: 50%;
    margin-top: 30px;

    color: #868f9e;
    font-weight: 500;
    font-size: 17px;
  }
  .jour__degre  {
    font-weight: 900;
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
</style>
