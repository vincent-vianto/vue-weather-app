<template>
    <div class="detailWrapper">
        <div class="row">
            <div class="col-6 col-lg-4">
                <div class="detailBlock">
                    <div class="iconWithText">
                        <h4>Wind</h4>
                    </div>
                    <div class="iconWithText">
                        <img :src="getIcon('wind')" alt='wind' width="40" height="40" />
                    </div>
                    <h6>{{Math.round(detail.wind)}} m/s</h6>
                </div>
            </div>
            <div class="col-6 col-lg-4">
                <div class="detailBlock">
                    <div class="iconWithText">
                        <h4>Sunrise</h4>
                    </div>
                    <div class="iconWithText">
                        <img :src="getIcon('sunrise')" alt='sunrise' width="40" height="40" />
                    </div>
                    <h6>{{getTime(detail.sunrise)}}</h6>
                </div>
            </div>
            <div class="col-6 col-lg-4">
                <div class="detailBlock">
                    <div class="iconWithText">
                        <h4>Sunset</h4>
                    </div>
                    <div class="iconWithText">
                        <img :src="getIcon('sunset')" alt='sunset' width="40" height="40"/>
                    </div>
                    <h6>{{getTime(detail.sunset)}}</h6>
                </div>
            </div>
            <div class="col-6">
                <div class="detailBlock">
                    <div class="iconWithText">
                        <h4>Humidity</h4>
                    </div>
                    <div class="iconWithText">
                        <img :src="getIcon('droplet')" alt='droplet' width="40" height="40"/>
                    </div>
                    <h6>{{detail.humidity}}%</h6>
                </div>
            </div>
            <div class="col-6">
                <div class="detailBlock">
                    <div class="iconWithText">
                        <h4>Cloudiness</h4>
                    </div>
                    <div class="iconWithText">
                        <img :src="getIcon('cloudy')" alt='cloudy' width="40" height="40"/>
                    </div>
                    <h6>{{detail.clouds}}%</h6>
                </div>
            </div>
        </div>
    </div>
</template>
    
<script>
import moment from 'moment'

import './style.css'
import 'animate.css'
import { icons } from '../../middleware/importAssets'


export default {
    name: 'DetailWeather',
    props: {
        detail: {}
    },
    methods: {
        getTime(time){
            return moment.utc(time, 'X').add(this.detail.timezone, 'seconds').format('LT')
        },
        getIcon(icon) {
            return icons[icon + '.svg']
        },
    },
}
</script>
  