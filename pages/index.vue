<template>
  <div>
    <div>{{msg}}</div>
    <img :src="imgSrc" />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      imgSrc: '',
      msg: '默认'
    }
  },
  mounted() {
    this.$axios.get('/api/yzm', {responseType: 'arraybuffer'}).then( (res) => {
      let src = 'data:image/png;base64,' + btoa(new Uint8Array(res.data).reduce((data, byte) => data + String.fromCharCode(byte), ''))
      this.imgSrc = src;
    });
    let params = {};
    this.$axios.post('/api/login', params).then((res) => {
      console.log(res);
    }).catch((error) => {
      console.log(error);
    });
  },
  asyncData ({ params }) {
    let param = {};
    return axios({
      method: 'post',
      url: 'http://yuecai2015.vicp.io/login',
      data: param
    }).then((res) => {
      return {msg: res.data.msg}
    }).catch((error) => {
      console.error(error);
    });
  }
}
</script>

<style>

</style>
