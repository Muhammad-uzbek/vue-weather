<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 23 ? 'warm' : '' ">
    <div class="main">
      <div class="search-box">
          <input 
          type="text" 
          class="search-bar" 
          placeholder="Search.." 
          v-model="query"
          @keypress="fetchWeather"/>
      </div>
      <Card  v-if="weather!=''" class="card" :weatherprop="weather"/>
    </div>
      <div class="side">
        <ul>
          <li v-for="region in regionsOfUzb" :key="region" @mouseover="fetchOnMouseOver">
            {{region}}
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'
export default {
    name:'app',
    components:{Card},
    data(){
        return{
            api_key:'79946b6e9a2cbe91e515ffe5635089a2',
            url_base:'https://api.openweathermap.org/data/2.5/',
            query:'',
            weather:"",
            regionsOfUzb:['Tashkent','Namangan','Andijon','Bukhara','Fergana','Jizzakh','Karakalpakstan','Kashkadarya','Navoiy','Samarkand','Sirdaryo','Surkhondaryo'],
            selectedRegion:'Tashkent'
        }
    },
    methods: {
      fetchWeather(e){
        if(e.key == 'Enter'){
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}&lang=pt_br`)
          .then(res =>{
            return res.json()
          }).then(this.setResults)
        }
      },
      fetchOnMouseOver(e){
        this.query=e.target.innerText;
        if(e.type == 'mouseover'){
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}&lang=pt_br`)
          .then(res =>{
            return res.json()
          }).then(this.setResults)
        }
      },
      setResults(results){
        this.weather = results;
      }
    },

}
</script>

<style>

*{
    margin:0;
    padding: 0;
    
}

body{
    font-family: 'montserrat', sans-serif;
}

#app{
  background-image:url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.3s;
  width: 100vw;
  height: 100vh;
  display: flex;
}


#app.warm{
  background-image: url('./assets/warm-bg.jpg');
}
.card{
  margin-top: 10px;
  width: 300px;
  height: auto;
}
.main{
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  width: 70%;
}
/* 20px bordered blured grey input */
.search-bar{
  position: relative;
  margin: 10px;
  border: 1px solid #ccc;
  border-radius: 20px;
  padding: 10px;
  width: 300px;
  height: auto;
  background-color: #fff;
  box-shadow: 0px 0px 5px #ccc;
}
.search-box{
  display: flex;
  justify-content: center;
}
.side{
  width: 30%;
  height: 100%;
  background-color: rgba(106, 106, 106, 0.295);
  backdrop-filter: blur(5px);
}
.side ul{
  list-style: none;
  padding: 10px;
  margin: 0;
  display: flex;
  flex-direction: column;
}
.side ul li{
  font-size: 18px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  cursor: pointer;
  color: #fff;
  padding: 10px;
  border-radius: 10px;
}
.side ul li:hover{
  background: rgba(172, 172, 172, 0.705);
}
</style>

