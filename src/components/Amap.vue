<script lang="ts">
import loadJs from '../helper/loadJs'
import { Zoom11, NJ_lNG_LAT } from '../constant/index'
export default {
    mounted() {
        console.log(5, Zoom11)
        loadJs('https://webapi.amap.com/loader.js').then((res) => {
            console.log(7, res)
            // 加载成功，进行后续操作
            AMapLoader.load({
                "key": "c1454bd34c55c4d74d11b2f025e28d3f",   // 申请好的Web端开发者Key，首次调用 load 时必填
                // "version": "2.0",   // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
                "plugins": ['AMap.Scale', 'AMap.ToolBar', 'AMap.MapType'],           // 需要使用的的插件列表，如比例尺'AMap.Scale'等
                "AMapUI": {             // 是否加载 AMapUI，缺省不加载
                    "version": '1.1',   // AMapUI 版本
                    "plugins":['overlay/SimpleMarker'],       // 需要加载的 AMapUI ui插件
                },
                // "Loca":{                // 是否加载 Loca， 缺省不加载
                //     "version": '2.0'  // Loca 版本
                // },
            }).then((AMap)=>{
                console.log(21, AMap)
                var map = new AMap.Map('amap-box', {
                    // viewMode: '2D', // 默认使用 2D 模式，如果希望使用带有俯仰角的 3D 模式，请设置 viewMode: '3D',
                    zoom: Zoom11, //初始化地图层级
                    center: [NJ_lNG_LAT.lng, NJ_lNG_LAT.lat] //初始化地图中心点
                });
                map.addControl(new AMap.Scale());
                map.addControl(new AMap.ToolBar());
                map.addControl(new AMap.MapType());

                map.on("complete", function(){
                    console.log("地图加载完成！");  
                });

                app.config.globalProperties.$map = map;
            }).catch((e)=>{
                console.error(e);  //加载错误提示
            }); 
        })
    }
}
</script>

<template>
  <div id="amap-box" class="map"></div>
</template>

<style>
.map {
    height: 100%;
    width: 100%;
    margin: 0;
}
</style>
