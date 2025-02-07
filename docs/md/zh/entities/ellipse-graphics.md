# 椭圆形(体)

`ellipse-graphics` 椭圆形(体)组件，作为`entity`的子组件添加包含 椭圆形(体)对象的实体到场景。描述由中心点和半长轴和半短轴定义的椭圆。 椭圆符合地球仪的曲率，可以放置在地面上或海拔高度，并且可以选择性地挤压成一个体积。 中心点由包含实体确定，如示例所示。

## 示例

### 添加椭圆形(体)到场景

#### 预览

<doc-preview>
  <template>
    <div class="viewer">
      <cesium-viewer @ready="ready">
        <entity :position="position1" :description="description" :ellipse.sync="ellipse1">
          <ellipse-graphics :semiMinorAxis="300000.0" :semiMajorAxis="300000.0" :height="200000.0" :material="material1"
            :outline="true"></ellipse-graphics>
        </entity>
        <entity :position="position2" :description="description" :ellipse.sync="ellipse2">
          <ellipse-graphics :semiMinorAxis="250000.0" :semiMajorAxis="400000.0" :material="material2"></ellipse-graphics>
        </entity>
        <entity :position="position3" :description="description" :ellipse.sync="ellipse3">
          <ellipse-graphics :semiMinorAxis="150000.0" :semiMajorAxis="300000.0" :extrudedHeight="200000.0" :rotation="rotation3" :material="material3"
            :outline="true"></ellipse-graphics>
        </entity>
      </cesium-viewer>
    </div>
  </template>

  <script>
    export default {
      data () {
        return {
          description: 'Hello Vue Cesium',
          ellipse1: {},
          position1: { lng: 111.0, lat: 40.0, height: 150000.0 },
          material1: 'GREEN',

          ellipse2: {},
          position2: { lng: 103.0, lat: 40.0 },
          material2: undefined,

          ellipse3: {},
          position3: { lng: 95.0, lat: 40.0,  height: 100000.0 },
          rotation3: 0,
          material3: {}
        }
      },
      methods: {
        ready (cesiumInstance) {
          const {Cesium, viewer} = cesiumInstance
          this.material2 = Cesium.Color.RED.withAlpha(0.5)

          this.material3 = Cesium.Color.BLUE.withAlpha(0.5)
          this.rotation3 = Cesium.Math.toRadians(45)
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
      <entity :position="position1" :description="description" :ellipse.sync="ellipse1">
        <ellipse-graphics
          :semiMinorAxis="300000.0"
          :semiMajorAxis="300000.0"
          :height="200000.0"
          :material="material1"
          :outline="true"
        ></ellipse-graphics>
      </entity>
      <entity :position="position2" :description="description" :ellipse.sync="ellipse2">
        <ellipse-graphics :semiMinorAxis="250000.0" :semiMajorAxis="400000.0" :material="material2"></ellipse-graphics>
      </entity>
      <entity :position="position3" :description="description" :ellipse.sync="ellipse3">
        <ellipse-graphics
          :semiMinorAxis="150000.0"
          :semiMajorAxis="300000.0"
          :extrudedHeight="200000.0"
          :rotation="rotation3"
          :material="material3"
          :outline="true"
        ></ellipse-graphics>
      </entity>
    </cesium-viewer>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        description: 'Hello Vue Cesium',
        ellipse1: {},
        position1: { lng: 111.0, lat: 40.0, height: 150000.0 },
        material1: 'GREEN',

        ellipse2: {},
        position2: { lng: 103.0, lat: 40.0 },
        material2: undefined,

        ellipse3: {},
        position3: { lng: 95.0, lat: 40.0, height: 100000.0 },
        rotation3: 0,
        material3: {}
      }
    },
    methods: {
      ready(cesiumInstance) {
        const { Cesium, viewer } = cesiumInstance
        this.material2 = Cesium.Color.RED.withAlpha(0.5)

        this.material3 = Cesium.Color.BLUE.withAlpha(0.5)
        this.rotation3 = Cesium.Math.toRadians(45)
      }
    }
  }
</script>
```

## 属性

<!-- prettier-ignore -->
| 属性名 | 类型 | 默认值 | 描述 |
| ------------------------ | --------------------- | --------- | -------------------------------------------------------------------------------------------- |
| show | Boolean | `true` | `optional` 指定 ellipse 是否显示。 |
| semiMajorAxis | Number | | `optional` 指定 ellipse 长半轴。 |
| semiMinorAxis | Number | | `optional` 指定 ellipse 短半轴。 |
| height | Number | `0` | `optional` 指定 ellipse 高度。 |
| heightReference | Number | | `optional` 指定 ellipse 高度模式。 **NONE: 0, CLAMP_TO_GROUND: 1, RELATIVE_TO_GROUND: 2** |
| extrudedHeight | Number | | `optional` 指定 ellipse 拉伸高度。 |
| extrudedHeightReference | Number | | `optional` 指定 ellipse 拉伸高度模式。**NONE: 0, CLAMP_TO_GROUND: 1, RELATIVE_TO_GROUND: 2** |
| rotation | Number | `0.0` | `optional` 指定 ellipse 正北逆时针旋转角度。 |
| stRotation | Number | `0.0` | `optional` 指定 ellipse 纹理正北逆时针旋转角度。 |
| granularity | Number | | `optional` 指定每个经纬度之间的采样粒度。 |
| fill | Boolean | `true` | `optional` 指定 ellipse 是否填充材质。 |
| material | Object\|String\|Array | `'white'` | `optional` 指定 ellipse 材质。 |
| outline | Boolean | `false` | `optional` 指定 ellipse 是否绘制轮廓线。 |
| outlineColor | Object\|String\|Array | `'black'` | `optional` 指定 ellipse 轮廓线颜色。 |
| outlineWidth | Number | `1.0` | `optional` 指定 ellipse 轮廓线宽度。 |
| numberOfVerticalLines | Number | `16` | `optional` 指定 ellipse 沿轮廓周长绘制的垂直线数。 |
| shadows | Number | `0` | `optional` 指定 ellipse 是否投射接收每一个光源的阴影。**DISABLED: 0, ENABLED: 1, CAST_ONLY: 2, RECEIVE_ONLY: 3, NUMBER_OF_SHADOW_MODES: 4, RECEIVE_ONLY: 3** |
| distanceDisplayCondition | Object | | `optional` 指定 ellipse 随相机距离的显示条件。 **结构：{ near: number, far: number }** |
| classificationType | Number | `2` | `optional` 指定 ellipse 的贴地模式。 **TERRAIN: 0, CESIUM_3D_TILE: 1, BOTH: 2, NUMBER_OF_CLASSIFICATION_TYPES: 3** |
| zIndex | Number | | `optional` 指定 ellipse 顺序，没有高度和拉伸高度才有效。 |

---

- 官方文档 [EllipseGraphics](https://cesiumjs.org/Cesium/Build/Documentation/EllipseGraphics.html)

## 事件

| 事件名            | 参数             | 描述                                                |
| ----------------- | ---------------- | --------------------------------------------------- |
| ready             | {Cesium, viewer} | 该组件渲染完毕时触发，返回 Cesium 类, viewer 实例。 |
| definitionChanged |                  | 每当更改或修改属性或子属性时触发该事件。            |
