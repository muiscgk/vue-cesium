# 经纬格网 Provider

`grid-imagery-provider`

## 示例

### 添加经纬格网图层到场景

#### 预览

<doc-preview>
  <template>
    <div class="viewer">
      <cesium-viewer @ready="ready">
        <imagery-layer :alpha="alpha" :brightness="brightness" :contrast="contrast">
          <grid-imagery-provider></grid-imagery-provider>
        </imagery-layer>
      </cesium-viewer>
      <div class="demo-tool">
        <span>透明度</span>
        <vue-slider v-model="alpha" :min="0" :max="1" :interval="0.01"  ></vue-slider>
        <span>亮度</span>
        <vue-slider v-model="brightness" :min="0" :max="3" :interval="0.01"  ></vue-slider>
        <span>对比度</span>
        <vue-slider v-model="contrast" :min="0" :max="3" :interval="0.01"  ></vue-slider>
      </div>
    </div>
  </template>

  <script>
    export default {
      data () {
        return {
          alpha: 1,
          brightness: 1,
          contrast: 1
        }
      },
      methods: {
        ready (cesiumInstance) {
          const {Cesium, viewer} = cesiumInstance
          // ...
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
        <grid-imagery-provider></grid-imagery-provider>
      </imagery-layer>
    </cesium-viewer>
    <div class="demo-tool">
      <span>透明度</span>
      <vue-slider v-model="alpha" :min="0" :max="1" :interval="0.01"></vue-slider>
      <span>亮度</span>
      <vue-slider v-model="brightness" :min="0" :max="3" :interval="0.01"></vue-slider>
      <span>对比度</span>
      <vue-slider v-model="contrast" :min="0" :max="3" :interval="0.01"></vue-slider>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        alpha: 1,
        brightness: 1,
        contrast: 1
      }
    },
    methods: {
      ready(cesiumInstance) {
        const { Cesium, viewer } = cesiumInstance
        // ...
      }
    }
  }
</script>
```

## 属性

<!-- prettier-ignore -->
| 属性名 | 类型 | 默认值 | 描述 |
| ----- | -------- | ------- | ------------------------------------- |
| tilingScheme | Object | | `required` 指定瓦片坐标系信息。 |
| ellipsoid | Object | | `optional` 指定参考椭球体。默认参考椭球WGS84。 |
| cells | Number | `8` | `optional` 指定网格单元格数量。 |
| color | Object\|String\|Array | `[1.0, 1.0, 1.0, 0.4]` | `optional` 指定网格线的颜色。 |
| glowColor | Object\|String\|Array | `[0.0, 1.0, 0.0, 0.05]` | `optional` 指定网格线发光的颜色。 |
| glowWidth | Number | `6` | `optional` 指定渲染发光效果的宽度。 |
| backgroundColor | Object\|String\|Array | `[0.0, 0.5, 0.0, 0.2]` | `optional` 指定填充背景色。 |
| tileWidth | Number | `256` | `optional` 指定瓦片到最详细级别的宽度。 |
| tileHeight | Number | `256` | `optional` 指定瓦片到最详细级别的高度。 |
| canvasSize | Number | `256` | `optional` 指定渲染画布大小。 |

- 官方文档 [GridImageryProvider](https://cesiumjs.org/Cesium/Build/Documentation/GridImageryProvider.html)

## 事件

| 事件名       | 参数              | 描述                                                                |
| ------------ | ----------------- | ------------------------------------------------------------------- |
| ready        | {Cesium, viewer}  | 该组件渲染完毕时触发，返回 Cesium 类, viewer 实例。                 |
| errorEvent   | TileProviderError | 当图层的提供者发生异步错误时触发, 返回一个 TileProviderError 实例。 |
| readyPromise | ImageryProvider   | 当图层可用时触发, 返回 ImageryProvider 实例。                       |
