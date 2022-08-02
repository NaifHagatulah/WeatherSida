<template>
  <div id="app">
   <main>
    <div class="seach-box">
      <input 
      type="text" 
      class="seach-bar" 
      placeholder="Seach..."
      v-model = "query"
      @keypress="featchWeather"
      
      />
      
      
    </div>
      
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}},{{weather.sys.country}}</div>
          <div class="date">RIGHT NOW</div>
        </div>
        
        <div class="weather-box">
          <div class="temp">{{weather.main.temp}}</div>
          <div class="weather">{{weather.weather[0].description}}</div>
        </div>
      </div>
   </main>
  </div>
</template>

<script>







export default {
  name: 'App',
  data(){
    return{
        backgroundimage: 'snow',
        api_key: "2ae77795bfe93e7c09734074923b9ad7",
        url_base: "https://api.openweathermap.org/data/2.5/",
        query:'',
        weather: {},
        location: {}
        
    }
  },
  methods:{
          
      
        featchWeather(e){
             
             if(e.key == "Enter" ){
              this.array = this.query.split(" ")
              fetch('https://api.openweathermap.org/data/2.5/weather?lat=' + location.lat + '&lon='+ location.lon +'&appid=2ae77795bfe93e7c09734074923b9ad7&units=metric')
              .then(res => {
                return res.json();
              }).then(this.setResults);
              fetch('http://api.openweathermap.org/geo/1.0/direct?q='+ this.array[0] + '&appid=2ae77795bfe93e7c09734074923b9ad7')
              .then(location =>{
                return location.json();
              }).then(this.setResults)
            }
        },
        setResults (results, location){
          this.location = location;
          this.weather = results;
          console.log(this.query);
          console.log(this.array[2]);
          console.log(this.weather);
          console.log(this.location.name.lat)
        },

      }
    }
</script>

<style>
*{
  margin:0 ;
  padding: 0;
  box-sizing: border-box;

}

body{
  font-family: 'montserrat', sans-serif;
}

#app {

  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
 }
main{
  min-height: 100vh;
  padding: 25px;
  background-image:linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}

.seach-box {
  width: 100%;
  margin-bottom: 30px;
  
}
.seach-box .seach-bar{
  display: block;
  width: 100%;
  padding: 25px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color:rgba(255,255,255,0.5);
  border-radius:0px 16px 0px 16px ;
  transition: 00.4s;
}

.seach-box .seach-bar:focus{
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.75);
  border-radius: 16px 0px 16px 0px;

}

.location-box .location{
  color: white ;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 0px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date{
  color: white ;
  font-size: 23px;
  font-weight: 300;
  text-align: center;
  text-emphasis-style: italic;
}
.weather-box{
  text-align: center;
}

.weather-box .temp{
display: inline-block;
padding: 10px 25px;
color: white;
font-size: 102px;
font-weight: 900;
text-shadow: 3px 6px rgba(255,255,255,0.25);
background-color: rgba(255,255,255,0.25);
border-radius: 16px;
margin: 30px 0px;
box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather{
color: #fff;
font-size: 48px;
font-weight: 700;
font-style: italic;
text-shadow: 3px 6x rgba(0, 0, 0, 0.25);
}
</style>
