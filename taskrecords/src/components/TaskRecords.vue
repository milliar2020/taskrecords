<template>
  <section>
    <div class="title">任务登记表</div>
    <div class="tips" style="text-align:left">返款时间：<br/>
    如有问题请联系客服。如果没有收到返款，请联系表单在线客服或者放单的微信。谢谢配合!</div>
    <el-form :model="taskRecordsForm" :rules="taskRecordsFormRules" ref="taskRecordsForm" class="task-record-form">
      <el-form-item label="微信账号" prop="wxAccount">
        <el-input
          v-model="taskRecordsForm.wxAccount"
          placeholder="请填写接单的微信号">
        </el-input>
      </el-form-item>
      <el-form-item label="手机号" prop="phoneNum">
        <el-input
          v-model="taskRecordsForm.phoneNum"
          placeholder="填写本人真实手机号">
        </el-input>
      </el-form-item>
      <el-form-item label="淘宝会员名" prop="taobaoAccount">
        <el-input
          v-model="taskRecordsForm.taobaoAccount"
          placeholder="填写做单的旺旺ID，不允许换号">
        </el-input>
      </el-form-item>
      <el-form-item label="地理位置" prop="adress">
        <div>
          <el-tag type="info" style="text-align: center">{{adress}}</el-tag>
        </div>
        <div>
          <el-tag type="info">经度:{{lng}}</el-tag>
          <el-tag type="info">维度:{{lat}}</el-tag>
        </div>
        <el-form-item>
          <el-button type="primary" icon="el-icon-location" circle @click="getLocation"></el-button>
        </el-form-item>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('taskRecordsForm')">提交</el-button>
      </el-form-item>
    </el-form>
  </section>
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
      lng: 0,
      taskRecordsForm: {
        wxAccount: '',
        phoneNum: '',
        taobaoAccount: '',
        adress: ''
      }
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
.title {
  margin-bottom: 30px;
  font-size: 16px;
}
.tips {
  color: #ff6633;
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
