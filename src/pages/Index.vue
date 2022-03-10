<template>
  <q-page class="flex column" :class="bgClass">
    <div class="col q-pt-lg q-px-md">
      <q-input
        v-model="search"
        @keyup.enter="getWeatherBySearch"
        placeholder="Поиск"
        borderless
        dark>
        <template v-slot:before>
          <q-icon
            @click="getLocation"
            name="my_location" />
        </template>
        <template v-slot:append>
          <q-btn
            @click="getWeatherBySearch"
            round
            dense
            flat
            icon="search" />
        </template>
      </q-input>
    </div>
    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          {{ weatherData.name }}
        </div>
        <div class="text-h6 text-weight-light">
          {{ weatherData.weather[0].main }}
        </div>
        <div class="text-h1 text-weight-thin" q-my-lg relative-position>
          <span>{{ Math.round(weatherData.main.temp) }}</span>
          <span class="text-h4 relative-position degree">&deg;C</span>
        </div>
      </div>
      <div class="col text-center">
        <img :src="`http://openweathermap.org/img/wn/${ weatherData.weather[0].icon }@2x.png`">
      </div>
    </template>
    <template v-else>
      <div class="col column text-white text-center">
        <div class="text-h2 text-weight-thin">
          Weather<br>Training App
        </div>
        <q-btn
          @click="getLocation"
          class="col"
          flat>
          <q-icon left size="3em" name="my_location" />
          <div>Определить свое местоположение</div>
        </q-btn>
      </div>
      <div class="col text-center">
        <img src="https://www.fillmurray.com/100/100" alt="Bill">
      </div>
    </template>
    <div class="col skyline">
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      search: '',
      weatherData: null,
      lat: null,
      lon: null,
      apiUrl: 'https://api.openweathermap.org/data/2.5/weather',
      apiKey: 'fdd175c1efdc932c7b38b1889aece29a',
      info: null
    }
  },
  computed: {
    bgClass () {
      if (this.weatherData) {
        if (this.weatherData.weather[0].icon.endsWith('n')) {
          return 'bg-night'
        } else {
          return 'bg-day'
        }
      }
    }
  },
  methods: {
    getLocation () {
      this.$q.loading.show()
      navigator.geolocation.getCurrentPosition(
        position => {
          this.lat = position.coords.latitude
          this.lon = position.coords.longitude
          this.getWeatherByCoords()
        })
    },
    getWeatherByCoords () {
      // eslint-disable-next-line no-template-curly-in-string
      this.$q.loading.show()
      this.$axios(`${this.apiUrl}?lat=${this.lat}&lon=${this.lon}&appid=${this.apiKey}&units=metric`).then(response => {
        this.weatherData = response.data
        this.$q.loading.hide()
      })
    },
    getWeatherBySearch () {
      // eslint-disable-next-line no-template-curly-in-string
      this.$q.loading.show()
      this.$axios(`${this.apiUrl}?q=${this.search}&appid=${this.apiKey}&units=metric`).then(response => {
        this.weatherData = response.data
        this.$q.loading.hide()
      })
    }
  }
}
</script>
<style lang="scss">
.q-page {
background: linear-gradient(to top, #222131, #302b63, #43439b)
&.bg-night
background: linear-gradient(to bottom, #232526, #414345)
&.bg-day
background: linear-gradient(to bottom, #b1bfc5, #d9b660)
}
.degree {
  top: -44px;
}
.skyline {
  flex: 0 0 100px;
  background: url("../assets/static.png");
  background-size: contain;
  background-position: center bottom;
}
</style>
