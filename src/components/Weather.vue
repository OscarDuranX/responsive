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
            <div class="text">
                <div class="precipitation">Precipitation: {{precipitation}}</div>
                <div class="humidity">Humidity: {{humidity}}</div>
                <div class="wind">Wind: {{wind}}</div>
                <div class="pollen">Pollen: {{pollen}}</div>
            </div>
        </div>
        <div class="forecast">
            <div class="forecast-day" v-for="forecast in forecasts">
                <div class="date">{{forecast.date}}</div>
                <div class="icon" :class="forecast.icon"></div>
                <div class="high-temp">{{forecast.highTemp}}</div>
                <div class="scale">º</div>
                <div class="low-temp">{{forecast.lowTemp}}</div>
                <div class="scale">º</div>
                <div class="forecast-pollen">Pollen {{forecast.pollen}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'weather',
  data () {
    return {
      connecting: true,
      location: 'New York, NY',
      date: 'Tuesday, April 15th',
      description: 'desc here',
      temp: 25,
      precipitation: '100%',
      humidity: '97%',
      wind: '4mph SW',
      pollen: 36,
      forecasts: []
    }
  },
  created: function () {
    this.fetchWeather()
  },
  methods: {
    fetchWeather: function () {
      this.$http.get('https://oscarduranx.github.io/responsive/weatherFakeAPI/weahterFaker.json').then((response) => {
        this.connecting = false
        this.forecasts = response.data
      }, (response) => {
        this.connecting = false
        this.showConnectionError()
      })
    },
    showConnectionError: function () {
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .weather {
    padding: 20px;
  }
  @media (min-width: 700px) {
    .weather {
      width: 700px;
    }
  }
  .location {
    font-size: 3em;
    color: black;
  }
  .date {
    font-size: 1.5em;
  }
  .description {
    font-size: 1.1em;
  }
  .current {
    overflow: auto;
    width: 100%;
  }
  .visual {
   float: left;
   width: 50%;
  }
  .text {
    float: right;
    width: 50%;
  }
  .forecast-day {
    display: inline-block;
    width: 14.285%;
  }
  @media (max-width: 650px) {
    .forecast-day {
      display: block;
      border-top: 1px solid black;
      width: 100%;
    }
  }
  .icon {
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
    height: 64px;
    width: 64px;
    margin: 0 auto;
  }
  .icon.cloudy {
    background-image: url('../assets/img/cloudy.png');
    position: left;
  }
  .icon.partly {
    background-image: url('../assets/img/partly_cloudy.png');
  }
  .icon.rain {
    background-image: url('../assets/img/rain_s_cloudy.png');
  }
  .icon.sunny {
    background-image: url('../assets/img/sunny.png');
  }
  .icon.thunderstorms {
    background-image: url('../assets/img/thunderstorms.png');
  }
  .visual .icon.cloudy {
    float: left;
    margin-left: 0;
  }
  .forecast-day div {
    vertical-align: middle;
    text-align: center;
  }
  .temp {
  }
  .high-temp, .low-temp {
    width: 50%;
    text-align: right;
  }
  .forecast-day .scale {
    width: 50%;
    text-align: left;
  }
  .forecast-day .date {
    font-size: 1em;
  }
  @media (max-width: 650px) {
    .date, .forecast-day .icon, .high-temp, .forecast-day .scale, .low-temp, .forecast-pollen {
      display: inline-block;
    }
    .date {
      color: black;
      font-weight: bold;
    }
    .high-temp, .forecast-day .scale, .low-temp {
      width: 20px;
    }
  }
</style>