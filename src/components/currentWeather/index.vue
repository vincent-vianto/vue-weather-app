<template>
  <div className="currentBlock">
    <div className="iconWithText">
      <img src="../../assets/icons/pin.svg" alt="pin" width="40" height="40" />
      <h3>{{weather.name}}</h3>
    </div>
    <div className="iconWithText">
      <h1>{{Math.round(weather.temp)}}&deg;C</h1>
      <img :src="icon" :alt="weather.icon" width='70' height='70' />
    </div>
    <h5>{{weather.description}}</h5>
    <small>
      {{currentTime}}
    </small>
  </div>
</template>
  
<script>
import moment from 'moment'

import './style.css'
import { icons } from '../../middleware/importAssets'


export default {
  name: 'currentWeather',
  props: {
    weather: {}
  },
  data() {
    return {
      icon: icons[this.weather.icon + '.svg'],
      currentTime: null,
    }
  },
  methods: {
    moment() {
      return moment();
    },
    updatedCurrent() {
      this.currentTime = moment()
        .utcOffset(this.weather.timezone / 60)
        .format('MMMM Do YYYY, h:mm:ss A')
    }
  },
  created() {
    setInterval(() => this.updatedCurrent(), 1000)
  }
}
</script>
