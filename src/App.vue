<template>
    <div id="app">
        <div class="md-form active-pink active-pink-2 mb-3 mt-0">
            <input class="form-control" type="text" placeholder="Search" 
            v-model="query"
            @keyup.enter="fetchweather"
            aria-label="Search">
        </div>
        <div v-if="typeof weather.main != 'undefined'">
          <h2>{{ weather.name }}, {{ weather.sys.country }}</h2>
        <h3>{{ dateBuilder() }}</h3>
        <h1>{{ weather.main.temp }}°</h1>
        <h2>{{ weather.weather[0].main }}</h2>
        </div>
        
    </div>
</template>
<script>
export default {
    name: 'App',
    data() {
        return {
            api_key: '27c83eb7a72052be755c3f0ae3081532',
            query: '',
            url_base: 'http://api.openweathermap.org/data/2.5/weather?q=',
            weather: {}


        }
    },
    methods : {
      fetchweather(){
        fetch(`${this.url_base}${this.query}&units=metric&appid=${this.api_key}`)
        .then(res=>{
          return res.json();}
          )
        .then(this.setResults);
      },
      setResults(results){
        this.weather=results;
      },
      dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
    }
}
</script>
<style>
</style>