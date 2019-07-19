<template>
    <div class="app">
        <div style="display:flex;position: absolute;height:100px;width:100px;background-color:red;float:left;left:100px">
            <img style="overflow:hidden;height:100px;width:100px" :src="logo"/>
        </div>
        <Row :gutter="16" class="contionRow" >
            <Col span="15" class="contion" style="padding:0px">
                <div id="divCol" class="divCol" @mouseenter="blurCol" @mouseleave="focusCol" >
                    <div v-for="(item,value,index) in objectArray" :key="item.id" class="music">
                        <Col span="12" class="message">
                            <div class="message" id="divMicMessage" ><!-- @mouseenter="blurMicMessage(index)" @mouseleave="focusMicMessage(index)"-->
                                <div><img style="overflow:hidden;height:120px;width:120px" :src="item.album.blurPicUrl"/></div>
                                <div class="musicMessage">
                                    <h3>{{item.name}}</h3>
                                    <p>{{item.artists[0].name}}</p>
                                </div>
                            </div>
                        </Col>
                    </div>
                </div>
            </Col>
        </Row>
    </div>
</template>
<script>

const API_PROXY = 'https://bird.ioliu.cn/v1/?url='
import axios from 'axios/index';
export default {
    name: 'app',
    data(){
        return{
            objectArray:[],
            logo:''
        }
    },
    methods:{
        blurCol(){
            const divCol = document.getElementById('divCol');
            divCol.style="box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.2)"
        },
        focusCol(){
            const divCol = document.getElementById('divCol');
            divCol.style="box-shadow: 0"
        },
        // blurMicMessage(){
        //     const divCol = document.getElementById('divMicMessage');
        //     divCol.style="box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.2)"
        // },
        // focusMicMessage(){
        //     const divCol = document.getElementById('divMicMessage');
        //     divCol.style="box-shadow: 0"
        // }
    },
    created(){
        axios.get(API_PROXY + 'http://music.163.com/api/playlist/detail?id=19723756')
        //成功返回
        .then(response=>{
            console.log(response);
            this.objectArray = response.data.result.tracks;
            this.logo = response.data.result.creator.avatarUrl;
        })
        //失败返回
        .catch(error=>{
            console.log(error);
        })
    }
}
</script>
<style>
.app{
    margin: 0;
    padding: 0;
    position: relative;
}
.contionRow{
    
    display: flex;
    justify-content: center;
    height: 800px;
}
.divCol{
    padding: 20px;
    border: 1px solid rgb(206, 206, 206);
    border-radius: 5px;
    height:800px;
    overflow: auto;
}
.music{
    text-align: left;
}
.message{
    display: flex;
    justify-content:start;
}
.musicMessage{
    margin:0 20px 0 20px
}
</style>

