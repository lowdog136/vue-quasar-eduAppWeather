<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input
        v-model="search"
        placeholder="Поиск"
        borderless
        dark>
        <template v-slot:before>
          <q-icon name="my_location" />
        </template>
        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>
    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          Kaliningrad
        </div>
        <div class="text-h6 text-weight-light">
          Rain
        </div>
        <div class="text-h1 text-weight-thin" q-my-lg relative-position>
          <span>8</span>
          <span class="text-h4 relative-position degree">&deg;</span>
        </div>
      </div>
      <div class="col text-center">
        <img src="https://www.fillmurray.com/100/100" alt="Bill">
      </div>
    </template>
    <template v-else>
      <div class="col column text-white text-center">
        <div class="text-h2 text-weight-thin">
          Quasar<br>Weather
        </div>
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
      weatherData: null
    }
  }
}
</script>
<style lang="scss">
.q-page {
background: linear-gradient(to top, #0f0c29, #302b63, #24243e )
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
