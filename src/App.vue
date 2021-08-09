<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        msg_data: []
      }
    },
    created() {
      this.initWebSocket();
      // this.initWebSocket2();

    },
    destroyed: function () {
      this.websocketclose();
    },
    methods: {
      initWebSocket2: function () {
        this.websock2 = new WebSocket("ws://localhost:8085/metricsDetailServer/vue_detail_endpoint");
        this.websock2.onopen = this.websocketonopen;
        this.websock2.onerror = this.websocketonerror;
        this.websock2.onmessage = this.websocketonmessage;
        this.websock2.onclose = this.websocketclose;
      },
      websocketonopen: function () {
        console.log("WebSocket连接成功");
      },
      websocketonerror: function (e) {
        console.log(e)
        console.log("WebSocket连接发生错误");
      },
      websocketonmessage: function (e) {
        var da = JSON.parse(e.data);
        console.log(da);
        this.msg_data.unshift(da);
      },
      websocketclose: function (e) {
        console.log("connection closed (" + e.code + ")");
      },
      initWebSocket: function () {
        this.websock = new WebSocket("ws://localhost:8085/metricsMainServer/vue_main_endpoint");
        this.websock.onopen = this.websocketonopen2;
        this.websock.onerror = this.websocketonerror2;
        this.websock.onmessage = this.websocketonmessage2;
        this.websock.onclose = this.websocketclose2;
      },
      websocketonopen2: function () {
        console.log("WebSocket连接成功");
      },
      websocketonerror2: function (e) {
        console.log(e)
        console.log("WebSocket连接发生错误");
      },
      websocketonmessage2: function (e) {
        var da = JSON.parse(e.data);
        console.log(da);
        this.msg_data.unshift(da);
      },
      websocketclose2: function (e) {
        console.log("connection closed (" + e.code + ")");
      }
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
