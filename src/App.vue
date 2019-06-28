<template>
  <div class="weatherWrap">
    <div class="bgImg">
      <img src="./assets/images/site-bg.jpg">
    </div>
    <appHeader :isVisible=isVisible :cityName=cityName :countryName=countryName></appHeader>
    <div class="weatherContent">      
      <div class="middle">
        <div class="searchWrap">
          <input type="search" name="search" placeholder="Search City" 
          v-model="searchCityKey" 
          v-on:keyup.enter="getCityWeather()">
          <a href="javascript:;" class="searchBtn" @click="getCityWeather()">Search</a>
        </div>  
        <div v-if="isVisible" class="cityWeatherInfo">
          {{ cityName }} weather forecast list 4 days / 3 hours apart
        </div>      
        <div class="results" v-if="isVisible">
          <div class="day" v-for="(item, index) in dataLength">
            <div>{{ apiData[index].dt_txt.slice(5, -3) }}</div>
            <div>{{ apiData[index].main.temp.toFixed(0) }}</div>
            <div><img :src="'http://openweathermap.org/img/w/' + apiData[index].weather[0].icon  + '.png'"></div>
            <div>{{ apiData[index].weather[0].description.toUpperCase() }}</div>
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
        dataLength : '',
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
      async getCityWeather() { 
      const response = await axios.get(`http://api.openweathermap.org/data/2.5/forecast?q=${this.searchCityKey}&appid=aa57ec0edb6274f21ccb4051b2411e3a&units=metric`);
      this.apiData = response.data.list;
      this.dataLength = this.apiData.length;
      this.cityName = response.data.city.name; 
      this.countryName = response.data.city.country; 
      this.isVisible = true;      
      }
    }
  }
</script>

<style lang="scss">
  @import './assets/css/main.scss'
</style>