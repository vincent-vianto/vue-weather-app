<template>
    <div className="mt-3">
        <h1 className="mb-2">Timeline</h1>
        <div className="forecastWrapper"  v-dragscroll>
            <div className="forecastBlock" v-for="(item,index) in forecast" :key="index">
                <h6>{{dayPicker(item.dt * 1000)}}</h6>
                <h6>{{formatClock(item.dt_txt)}}</h6>
                <img :src="getIcon(item.weather[0].icon)" alt={{item.weather[0].icon}} width="100" height="100"
                    draggable="false" />
                <h6>{{item.weather[0].description}}</h6>
            </div>
        </div>
    </div>
</template>
  
<script>
import moment from 'moment'

import './style.css'
import { icons } from '../../middleware/importAssets'
import { dragscroll } from 'vue-dragscroll'

export default {
    name: 'forecastWeather',
    props: {
        forecast: [],
    },
    directives: {
        dragscroll
    },
    methods: {
        moment() {
            return moment();
        },
        dayPicker(time) {
            const dateNow = moment(Date.now())
            const dateDt = moment(time)
            let dayDiff =
                dateNow.diff(dateDt, 'day') === 0
                    ? 'Today'
                    : dateNow.diff(dateDt, 'day') === -1
                        ? 'Tomorrow'
                        : dateDt.format('D MMM')
            return dayDiff
        },
        formatClock(time) {
            return moment(time).format('LT')
        },
        getIcon(icon) {
            return icons[icon + '.svg']
        },
    },
}
</script>


