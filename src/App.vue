<template>
  <div class="weatherWrap">
    <div class="bgImg">
      <img src="./assets/images/site-bg.jpg">
    </div>
    <appHeader :isVisible=isVisible :cityName=cityName :countryName=countryName></appHeader>
    <div class="weatherContent">      
      <div class="middle">
        <div class="searchWrap" v-if="!isVisible">
          <input type="search" name="search" placeholder="Search City" 
          v-model="searchCityKey" 
          v-on:keyup.enter="getCityWeather()">
          <a href="javascript:;" class="searchBtn" @click="getCityWeather()">Search</a>
        </div>  
        <div v-if="isVisible" class="cityWeatherInfo">
          {{ cityName }} 4 gün / 3 saat arayla hava durumu tahmin listesi
        </div>      
        <div class="results" v-if="isVisible">
          <div class="day" v-for="item in dForLoop">
            <div>{{ apiData.list[d].dt_txt.slice(5, -3) }}</div>
            <div>{{ apiData.list[d].main.temp.toFixed(0) }}</div>
            <div>
              <img :src="'http://openweathermap.org/img/w/' + apiData.list[d].weather[0].icon  + '.png'">
            </div>
            <div>
              {{ apiData.list[d].weather[0].description.toUpperCase() }}
            </div>
            <div class="dFoorLoopIncrease">{{ d++ }}</div>
          </div>
        </div>
      </div>
     </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import Header from './components/header';

  export default {
    data() {
      return {
        apiData : '',
        d : 0,
        dForLoop : 40,
        searchCityKey : '',
        isVisible : false,  
        cityName : '',
        countryName : ''
      }
    },
    components : {
      appHeader : Header
    },
    methods : {
      getCityWeather: function() {       
        var self = this;        
        axios.get('http://api.openweathermap.org/data/2.5/forecast?q=' + self.searchCityKey +'&appid=aa57ec0edb6274f21ccb4051b2411e3a&units=metric')
        .then(response => {                 
          self.apiData = response.data;
          self.cityName = response.data.city.name;        
          self.countryName = response.data.city.country;                  
          self.isVisible = true;
        });  
      }
    }
  }
</script>

<style lang="scss">
  @import './assets/css/main.scss'
</style>