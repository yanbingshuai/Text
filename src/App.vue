<template>
   <div id="app">
      <button @click="handleAlert">alert</button>
      <button @click="handleConfirm">confirm</button>
      <button @click="handleMsg">alert</button>
   </div>
</template>

<script>
import  Stomp from 'stompjs';
    import { MQTT_SERVICE, MQTT_USERNAME, MQTT_PASSWORD,MQTT_topic } from '@/utils/mqtt'
    export default {
        name: "App",
        data() {
            return{
                client: Stomp.client(MQTT_SERVICE)
            }
        },
        mounted(){
            this.connect();
        },

        methods:{
            onConnected:function(){
                //订阅的频道
                const topic = MQTT_topic;
                this.client.subscribe(topic,this.responseCallback,this.onFailed);
            },
            onFailed:function(msg){
                console.log("MQ Failed:" + msg);
            },
            //成功时的回调函数
            responseCallback:function(msg){
                //接收消息的处理
                console.log("MQ msg=>" + msg.body);
            },
            //连接
            connect:function(){
                const headers = {
                    login: MQTT_USERNAME,
                    password: MQTT_PASSWORD
                };
                this.client.connect(headers,this.onConnected,this.onFailed);
            },
        },
        watch:{

        }
    }
</script>
