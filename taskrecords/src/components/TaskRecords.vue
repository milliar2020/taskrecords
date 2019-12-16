<template>
  <div class="hello">
    <ul>
      <li>省份:{{province}}</li>
      <li>城市:{{city}}</li>
      <li>区县:{{district}}</li>
      <li>详细地址:{{adress}}</li>
      <li>纬度:{{lat}}</li>
      <li>经度:{{lng}}</li>
    </ul>
    <button v-on:click="getLocation">定位</button>
  </div>
</template>

<script>
import AMap from 'AMap'
import { location } from '../utils/locationutil'

export default {
  name: "TaskRecords",
  props: {
    msg: String
  },
  data () {
    return {
      city: '',
      province: '',
      district: '',
      adress: '',
      lat: 0,
      lng: 0
    }
  },
  methods: {
    getLocation () {
      let _that = this
      let geolocation = location.initMap('map-container') // 定位
      AMap.event.addListener(geolocation, 'complete', result => {
        _that.lat = result.position.lat
        _that.lng = result.position.lng
        _that.province = result.addressComponent.province
        _that.city = result.addressComponent.city
        _that.district = result.addressComponent.district
        _that.adress = result.formattedAddress
      })
    }
  },
  mounted () {
    this.getLocation() // 调用获取地理位置
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
