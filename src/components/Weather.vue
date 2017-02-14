<template>
  <div class="weather">
      <div class="location">{{location}}</div>
      <div class="date">{{date}}</div>
      <div class="description">{{description}}</div>
      <div class="current">
          <div class="visual">
              <div class="icon cloudy" alt="cloudy"></div>
              <div class="temp">{{temp}}</div>
              <div class="scale">º</div>
          </div>
      </div>
      <div class="text">
          <div class="precipitation">Precipitation: {{precipitation}}</div>
          <div class="humidity">Humidity: {{humidity}}</div>
          <div class="wind">Wind: {{wind}}</div>
          <div class="pollen">Pollen: {{pollen}}</div>
      </div>
      <div class="forecast">
          <div class="forecast-day" v-for="forecast in forecasts">
              <div class="date">{{ forecast.date }}</div>
              <div v-bind:class="'icon ' + forecast.icon"></div>
              <div class="low-temps">{{ forecast.lowtemps }}</div>
              <div class="high-temps">{{ forecast.hightemps }}</div>
          </div>
      </div>
  </div>
</template>
<style>
</style>
<script>
export default{
  name: 'weather',
  data () {
    return {
      location: 'New York, NY',
      date: 'Tusday, April 15th',
      description: 'desc here',
      temp: 25,
      precipitation: '100%',
      humidity: '97%',
      wind: '4 mph SW',
      pollen: 36,
      forecasts: [

      ],
      prova: []
    }
  },
  methods: {
    fetchWeather: function () {
      this.$http.get('http://localhost:3000/weather').then((response) => {
        console.log(response)
        this.forecasts = response.data
      }, (response) => {

      })
    }
  },
  created: function () {
    this.fetchWeather()
  }
}
</script>

<style scoped>
  .weather {
    width: 100%;
    padding: 20px;
    box-shadow: 0 100px 100px rgba(0,0,0,0.2);
  }
  @media (min-width: 700px) {
    .weather {
      width: 700px;
    }
  }


  .location {
    font-size: 3em;
  }
  .date {
    font-size: 1.5em;
  }
  .description {
    font-size: 1.1em;
  }
  .current {
    overflow: auto;
    width: 100%,
  }
  .visual {
    float:left;
    width: 50%,
  }
  .visual .icon {
    width: 64px;
    height: 64px;
    text-align: center;
  }

  .text {
    float:right;
    width: 50%,
  }
  .forecast-day {
    display:inline-block;
    width: 14.2857%;
    text-align: center;
  }

  .forecast-day .icon{
    width: 64px;
    height: 64px;

  }

  .icon{
    background-repeat: no-repeat;
    background-size: contain;
    display: inline-block;

  }
  .icon.cloudy {
    background-image: url("../assets/img/cloudy.png");
  }
  .icon.partlycloudy {
    background-image: url('../assets/img/partly_cloudy.png');
  }
  .icon.sunny {
    background-image: url('../assets/img/sunny.png');
  }
  .icon.rain {
    background-image: url('../assets/img/rain.png');
  }
  .icon.rainscloudy {
    background-image: url('../assets/img/rain_s_cloudy.png');
  }
  .icon.thunderstorms {
    background-image: url('../assets/img/thunderstorms.png');
  }

  @media (min-width: 650px) {
    .location {
      font-size: 5em;
      color:green;
    }
    .date, .icon, .high-temp, .low-temp {
      display:inline-block;
    }
    .forecast-day .date{
    width: 50%;
    text-align: left;

    }
  }

</style>