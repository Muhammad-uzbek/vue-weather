<template>
    <div id="card"> 
        <div class="img-wrap">
            <img v-if="weatherprop" :src="weatherimg" alt="weather"> 
        </div>
        <div class="bottom">
            <div class="weather-data">
                <h3>{{weatherprop.weather[0].main||'none'}}</h3>
                <div class="second">
                    <p>{{Math.round(weatherprop.main.temp)||'none'}}&deg;C</p>
                    <p class="city">{{weatherprop.name||'none'}}</p>
                </div>
            </div>
            <div class="date">
                <p>{{date()||'none'}}</p>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name:'Card',
    props:['weatherprop'],
    data(){
        return{
            weatherimg: this.weatherprop!='' ? 'http://openweathermap.org/img/w/'+this.weatherprop.weather[0].icon+'.png' : 'https://picsum.photos/400',
            isHot: (Math.round(this.weatherprop.main.temp > 20)) ? true : false ,
            date: function(){
                var date = new Date();
                var day = date.getDate();
                var month = date.getMonth()+1;
                var months = ['','Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
                return day+' '+months[month];
                }
        }
    },
}
</script>
<style>
    #card{
        width:350px;
        height: 100px;
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        box-sizing: border-box;
        background-color:rgba(160, 160, 160, 0.577);
        backdrop-filter: blur(10px);
        border-radius:20px;
    }
    .img-wrap{
        width:300px;
        height: 50%;
        display: flex;
        justify-content: center;
    }
    .img-wrap img{
        width:50px;
        height:50px;
        margin: 0 auto;
        padding: 0 auto;
    }
    .bottom{
        width:100%;
        height:50%;
        display:flex;
        flex-direction:row;
        justify-content:space-between;
        align-items:center;
        
    }
    .bottom .weather-data{
        width:70%;
        height: 100%;
        display: flex;
        background-color:rgba(34, 34, 34, 0.507);
        box-sizing: border-box;
        color:white;
        justify-content: center;
        padding: 5px;
        border-bottom-left-radius: 20px;
    }
    .bottom .weather-data h3{
        font-size:1.5em;
        margin:0;
        line-height:50px;
        width:50%;
        height: 100%;
        text-align: center;
    }
    .bottom .weather-data .second{
        width:50%;
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        padding-left: 10px;
    }
    .city{
        font-size: 12px;
        margin:0;
    }
    .date{
        width: 30%;
        height: 100%;
        background-color: rgba(172, 255, 47, 0.562);
        color: #fff;
        font: 12px;
        border-bottom-right-radius: 20px;
        line-height: 50px;
        text-align: center;
    }
    .date.hot{
        width: 30%;
        height: 100%;
        background-color: rgb(255, 127, 47);
        color: #fff;
        font: 12px;
        border-bottom-right-radius: 20px;
        line-height: 50px;
        text-align: center;
    }
@media screen and (max-width: 680px) {
    #card{
        width:250px;
    }
    .img-wrap{
        width:250px;
    }
    
}
</style>
