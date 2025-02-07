# WMS 服务 Provider

`wms-imagery-provider`作为`imagery-layer`子组件加载 WMS 服务的影像图层。

## 示例

### 添加 WMS 服务到场景

#### 预览

<doc-preview>
  <template>
    <div class="viewer">
      <cesium-viewer @ready="ready">
       <imagery-layer :alpha="alpha" :brightness="brightness" :contrast="contrast">
        <wms-imagery-provider :url="url" :layers="layers" :parameters="parameters"></wms-imagery-provider>
       </imagery-layer>
      </cesium-viewer>
      <div class="demo-tool">
        <span>透明度</span>
        <vue-slider v-model="alpha" :min="0" :max="1" :interval="0.01"  ></vue-slider>
        <span>亮度</span>
        <vue-slider v-model="brightness" :min="0" :max="3" :interval="0.01"  ></vue-slider>
        <span>对比度</span>
        <vue-slider v-model="contrast" :min="0" :max="3" :interval="0.01"  ></vue-slider>
        <span>切换图层</span>
        <md-select v-model="layers" placeholder="请选择服务" @selected="mdSelected">
          <md-option
            v-for="item in options"
            :key="item.value"
            :value="item.value">
            {{item.label}}
          </md-option>
        </md-select>
      </div>
    </div>
  </template>

  <script>
    export default {
      data () {
        return {
          url: 'https://www.ncei.noaa.gov/thredds/wms/gfs-004-files/201809/20180916/gfs_4_20180916_0000_000.grb2',
          layers: 'Precipitable_water_entire_atmosphere_single_layer',
          parameters: {
            ColorScaleRange: '0.1,66.8'
          },
          alpha: 1,
          brightness: 1,
          contrast: 1,
          options: [{
            label: 'WMS:Rainfall',
            value: 'Precipitable_water_entire_atmosphere_single_layer'
          }, {
            label: 'WMS:Air Pressure',
            value: 'Pressure_surface'
          }]
        }
      },
      methods: {
        ready (cesiumInstance) {
          const {Cesium, viewer} = cesiumInstance
          this.cesiumInstance = cesiumInstance
        },
        mdSelected (value) {
          if (value === 'Precipitable_water_entire_atmosphere_single_layer') {
            this.parameters = {
              ColorScaleRange: '0.1,66.8'
            }
          } else if (value === 'Pressure_surface') {
            this.parameters = {
              ColorScaleRange: '51640,103500'
            }
          }
        }
      }
    }
  </script>
</doc-preview>

#### 代码

```html
<template>
  <div class="viewer">
    <cesium-viewer @ready="ready">
      <imagery-layer :alpha="alpha" :brightness="brightness" :contrast="contrast">
        <wms-imagery-provider :url="url" :layers="layers" :parameters="parameters"></wms-imagery-provider>
      </imagery-layer>
    </cesium-viewer>
    <div class="demo-tool">
      <span>透明度</span>
      <vue-slider v-model="alpha" :min="0" :max="1" :interval="0.01"></vue-slider>
      <span>亮度</span>
      <vue-slider v-model="brightness" :min="0" :max="3" :interval="0.01"></vue-slider>
      <span>对比度</span>
      <vue-slider v-model="contrast" :min="0" :max="3" :interval="0.01"></vue-slider>
      <span>切换图层</span>
      <md-select v-model="layers" placeholder="请选择服务" @selected="mdSelected">
        <md-option v-for="item in options" :key="item.value" :value="item.value">
          {{item.label}}
        </md-option>
      </md-select>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        url: 'https://www.ncei.noaa.gov/thredds/wms/gfs-004-files/201809/20180916/gfs_4_20180916_0000_000.grb2',
        layers: 'Precipitable_water_entire_atmosphere_single_layer',
        parameters: {
          ColorScaleRange: '0.1,66.8'
        },
        alpha: 1,
        brightness: 1,
        contrast: 1,
        options: [
          {
            label: 'WMS:Rainfall',
            value: 'Precipitable_water_entire_atmosphere_single_layer'
          },
          {
            label: 'WMS:Air Pressure',
            value: 'Pressure_surface'
          }
        ]
      }
    },
    methods: {
      ready(cesiumInstance) {
        const { Cesium, viewer } = cesiumInstance
        this.cesiumInstance = cesiumInstance
      },
      mdSelected(value) {
        if (value === 'Precipitable_water_entire_atmosphere_single_layer') {
          this.parameters = {
            ColorScaleRange: '0.1,66.8'
          }
        } else if (value === 'Pressure_surface') {
          this.parameters = {
            ColorScaleRange: '51640,103500'
          }
        }
      }
    }
  }
</script>
```

## 属性

<!-- prettier-ignore -->
| 属性名 | 类型 | 默认值 | 描述 |
| ------------------------ | --------------- | ------ | ------------------------------------------------------------------------- |
| url | String\|Object | | `required` 指定 WMS 服务地址。 |
| layers | String | | `required` 指定服务图层，多个图层用","隔开。 |
| parameters | Object | | `optional` 在 GetMap URL 中传递给 WMS 服务器的其他参数。 |
| getFeatureInfoParameters | Object | | `optional` 在 GetFeatureInfo URL 中传递给 WMS 服务器的其他参数。 |
| enablePickFeatures | Boolean | `true` | `optional` 指定是否支持拾取对象，通过 GetFeatureInfo 获取，需要服务支持。 |
| getFeatureInfoFormats | Array | | `optional` 指定 WMS GetFeatureInfo 请求的格式。 |
| rectangle | Object | | `optional` 指定 WMS 图层矩形范围。 **结构：{ west: number, south: number, east: number, north: number }** |
| tilingScheme | Object | | `optional` 指定 WMS 服务瓦片投影参数。 |
| ellipsoid | Object | | `optional` 指定 WMS 服务椭球体参数，如果指定了 tilingScheme 此属性无效。 |
| tileWidth | Number | `256` | `optional` 指定像元宽度。 |
| tileHeight | Number | `256` | `optional` 指定像元高度。 |
| minimumLevel | Number | `0` | `optional` 指定图层可以显示的最小层级。 |
| maximumLevel | Number | | `optional` 指定图层可以显示的最大层级，undefined 表示没有限制。 |
| crs | String | | `optional` 指定 CRS 规范，用于 WMS 规范> = 1.3.0。 |
| srs | String | | `optional` 指定 SRS 规范，用于 WMS 规范 1.1.0 或 1.1.1 |
| credit | Credit\| String | | `optional` 指定服务描述信息。 |
| subdomains | String\| Array | `'abc'` | `optional` 指定服务子域 。 |
| clock | Object | | `optional` |
| times | Object | | `optional` |

---

- 官方文档 [WebMapServiceImageryProvider](https://cesiumjs.org/Cesium/Build/Documentation/WebMapServiceImageryProvider.html)

## 事件

| 事件名       | 参数              | 描述                                                                |
| ------------ | ----------------- | ------------------------------------------------------------------- |
| ready        | {Cesium, viewer}  | 该组件渲染完毕时触发，返回 Cesium 类, viewer 实例。                 |
| errorEvent   | TileProviderError | 当图层的提供者发生异步错误时触发, 返回一个 TileProviderError 实例。 |
| readyPromise | ImageryProvider   | 当图层可用时触发, 返回 ImageryProvider 实例。                       |
