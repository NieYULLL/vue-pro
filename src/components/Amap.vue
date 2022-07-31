<template>
  <div class="box">
    <div class="info">
      <div class="input-item">
        <div class="input-item-prepend">
          <span class="input-item-text" style="width:8rem;">请输入关键字</span>
        </div>
        <!-- <input id='tipinput' type="text" @change="handlerSearch"> -->
        <button @click="handlerSearch">click</button>
      </div>
    </div>
    <div id="container"></div>
    <div id="displayDiv" class="input-card">
    <h4>左击获取经纬度： </h4>
    <div >
      <input type="text" readonly="true" v-model="getPosition">
    </div>
</div>
  </div>

</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader'
const { AMap } = window
export default {
  data () {
    return {
      map: null,
      selectPointLng: null,
      selectPointLat: null
    }
  },
  computed: {
    getPosition: function () {
      const isNull = this.selectPointLat == null || this.selectPointLng == null
      return isNull ? '' : this.selectPointLat + ',' + this.selectPointLng
    }

  },
  mounted () {
    // DOM初始化完成进行地图初始化
    console.log('地图组件初始化')
    this.initMap()
  },
  methods: {
    initMap () {
      AMapLoader.load({
        key: 'bdb6feb606a60a1a60285cde90910b54', // 申请好的Web端开发者Key，首次调用 load 时必填
        version: '2.0', // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: ['AMap.ToolBar', 'AMap.Scale',
          'AMap.HawkEye',
          'AMap.MapType',
          'AMap.Geolocation', 'AMap.PlaceSearch'] // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      }).then((AMap) => {
        this.map = new AMap.Map('container', { // 设置地图容器id
          viewMode: '3D', // 是否为3D地图模式
          zoom: 12, // 初始化地图级别
          center: [116.38753, 40.014690] // 初始化地图中心点位置
        })
        this.map.on('click', this.mapClick)
        var toolbar = new AMap.ToolBar()
        this.map.addControl(toolbar)
        // 在图面添加比例尺控件，展示地图在当前层级和纬度下的比例尺
        // this.map.addControl(new AMap.Scale())

        // 在图面添加鹰眼控件，在地图右下角显示地图的缩略图
        // this.map.addControl(new AMap.HawkEye({ isOpen: true }))

        // 在图面添加类别切换控件，实现默认图层与卫星图、实施交通图层之间切换的控制
        // this.map.addControl(new AMap.MapType())

        // 在图面添加定位控件，用来获取和展示用户主机所在的经纬度位置
        // this.map.addControl(new AMap.Geolocation())
      }).catch(e => {
        console.log(e)
      })
    },
    mapClick (value) {
      this.selectPointLat = value.lnglat.lat
      this.selectPointLng = value.lnglat.lng
    },
    handlerSearch (e) {
      console.log(e)
      var marker = new AMap.Marker({
        position: new AMap.LngLat(this.selectPointLng, this.selectPointLat)
      })
      this.map.add(marker)
    }

  }
}
</script>

<style  scoped>
    .box{
      position: relative;
    }
    .box .info{
      position: absolute;
      z-index: 9;
      top: 1rem;
    }
    #container{
        padding:0px;
        margin: 0px;
        width: 100%;
        height: 500px;
    }

    html,body{
        width: 100%;
        height: 100%;
        margin: 0px;
    }
    .map{
        height: 100%;
        width: 100%;
        float: left;
    }
    .input-card {
        display: flex;
        flex-direction: column;
        min-width: 0;
        word-wrap: break-word;
        background-color: #fff;
        background-clip: border-box;
        border-radius: .25rem;
        width: 22rem;
        border-width: 0;
        border-radius: 0.4rem;
        box-shadow: 0 2px 6px 0 rgba(114, 124, 245, .5);
        position: absolute;
        bottom: 1rem;
        right: 1rem;
        -ms-flex: 1 1 auto;
        flex: 1 1 auto;
        padding: 0.75rem 1.25rem;
}

</style>
