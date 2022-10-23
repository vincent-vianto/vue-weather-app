<template>
  <div class="App" v-bind:style="getBackground(weather.id)">
    <div class="container mt-4">
      <SearchInput :handleSubmit="handleSubmit" :query="query" :handleChange="handleChange" />
      <div v-if="loading">
        <LoadingWrapper />
      </div>
      <div class="row animate__animated animate__fadeIn" v-if="!loading && showWeather">
        <div class="mt-3 col-12 col-md-6">
          <CurrentWeather :weather="weather" />
        </div>
        <div class="mt-3 col-12 col-md-6">
          <DetailWeather :detail="detail" />
        </div>
        <div class="mt-3 col-12">
          <Forecast :forecast="forecast" />
        </div>
      </div>
      <div v-if="error">
        <div class="animate__animated animate__fadeIn">
          <ErrorWrapper :errorMsg="errorMsg" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import './App.css'
import { apiCallCurrent, apiCallforecast } from './services'
import CurrentWeather from './components/currentWeather/index.vue';
import Forecast from './components/forecast/index.vue'
import DetailWeather from './components/detailWeather/index.vue'
import ErrorWrapper from './components/handlingWrapper/errorWrapper.vue'
import LoadingWrapper from './components/handlingWrapper/loadingWrapper.vue'
import SearchInput from './components/searchInput/index.vue';
import { imageWeather } from './middleware/imageWeather';

export default {
  name: "App",
  components: { CurrentWeather, Forecast, DetailWeather, SearchInput, ErrorWrapper, LoadingWrapper },

  data() {
    return {
      weather: {},
      detail: {},
      forecast: [],
      loading: false,
      showWeather: false,
      error: false,
      query: '',
      search: 'London',
      errorMsg: {}
    };
  },

  async mounted() {
    this.load()
  },
  watch: {
    'search': {
      handler() {
        this.load();
      },
      immediate: true
    }
  },
  methods: {
    async load() {
      try {
        this.loading = true
        const current = await apiCallCurrent(this.search)
        const forecast = await apiCallforecast(this.search)

        this.weather.id = current.data.weather[0].id

        this.weather.name = current.data.name + ', ' + current.data.sys.country
        this.weather.description = current.data.weather[0].description
        this.weather.main = current.data.weather[0].main
        this.weather.icon = current.data.weather[0].icon
        this.weather.temp = current.data.main.temp
        this.weather.timezone = current.data.timezone

        this.detail.clouds = current.data.clouds.all
        this.detail.humidity = current.data.main.humidity
        this.detail.wind = current.data.wind.speed
        this.detail.sunrise = current.data.sys.sunrise
        this.detail.sunset = current.data.sys.sunset
        this.detail.timezone = current.data.timezone

        this.forecast = forecast.data.list

        this.loading = false
        this.showWeather = true
        this.error = false
      } catch (error) {
        this.loading = false
        this.errorMsg = error.response.data
        this.showWeather = (false)
        this.error = true
      }
    },
    handleSubmit(event) {
      event.preventDefault();
      this.search = this.query
      this.query = ''
    },
    getBackground(id) {
      return imageWeather(id)
    },
    handleChange(event) { this.query = event.target.value },
  },

}
</script>

