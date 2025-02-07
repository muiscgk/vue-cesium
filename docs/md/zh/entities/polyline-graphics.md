# 折线

`polyline-graphics` 折线组件，作为`entity`的子组件添加包折线对象的实体到场景。折线对象描述的是折线，前两个位置定义线段，每个附加位置定义前一个位置的线段。 这些段可以是线性连接点，大弧度或夹紧到地形。如示例所示。

## 示例

### 添加线实体到场景

#### 预览

<doc-preview>
  <template>
    <div class="viewer">
      <cesium-viewer @ready="ready">
        <entity :polyline.sync="polyline1">
          <polyline-graphics :positions="positions1" :material="material1" :width="5" :clampToGround="false" heightPositions></polyline-graphics>
        </entity>
        <entity :polyline.sync="polyline2">
          <polyline-graphics :positions="positions2" :material="material2" :width="10"></polyline-graphics>
        </entity>
        <entity :polyline.sync="polyline3">
          <polyline-graphics :positions="positions3" :material="material3" :width="10"></polyline-graphics>
        </entity>
      </cesium-viewer>
    </div>
  </template>

  <script>
    export default {
      data () {
        return {
          polyline1: {},
          positions1: [{ lng: 90, lat: 20, height: 10000 }, { lng: 120, lat: 20, height: 10000 }],
          material1: undefined,
          polyline2: {},
          positions2: [{ lng: 90, lat: 30, height: 10000 }, { lng: 120, lat: 30, height: 10000 }],
          material2: undefined,
          polyline3: {},
          positions3: [],
          material3: undefined
        }
      },
      methods: {
        ready (cesiumInstance) {
          const {Cesium, viewer} = cesiumInstance
          this.material1 = Cesium.Color.RED
          this.material2 = new Cesium.PolylineGlowMaterialProperty({
            glowPower : 0.2,
            color : Cesium.Color.BLUE
          })
          this.material3 = new Cesium.PolylineArrowMaterialProperty(Cesium.Color.PURPLE)
          this.positions3 = [{ lng: 90, lat: 40, height: 10000 }, { lng: 120, lat: 40, height: 10000 }]
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
      <entity :polyline.sync="polyline1">
        <polyline-graphics
          :positions="positions1"
          :material="material1"
          :width="5"
          :clampToGround="false"
          heightPositions
        ></polyline-graphics>
      </entity>
      <entity :polyline.sync="polyline2">
        <polyline-graphics :positions="positions2" :material="material2" :width="10"></polyline-graphics>
      </entity>
      <entity :polyline.sync="polyline3">
        <polyline-graphics :positions="positions3" :material="material3" :width="10"></polyline-graphics>
      </entity>
    </cesium-viewer>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        polyline1: {},
        positions1: [{ lng: 90, lat: 20, height: 10000 }, { lng: 120, lat: 20, height: 10000 }],
        material1: undefined,
        polyline2: {},
        positions2: [{ lng: 90, lat: 30, height: 10000 }, { lng: 120, lat: 30, height: 10000 }],
        material2: undefined,
        polyline3: {},
        positions3: [{ lng: 90, lat: 40, height: 10000 }, { lng: 120, lat: 40, height: 10000 }],
        material3: undefined
      }
    },
    methods: {
      ready(cesiumInstance) {
        const { Cesium, viewer } = cesiumInstance
        this.material1 = Cesium.Color.RED
        this.material2 = new Cesium.PolylineGlowMaterialProperty({
          glowPower: 0.2,
          color: Cesium.Color.BLUE
        })
        this.material3 = new Cesium.PolylineArrowMaterialProperty(Cesium.Color.PURPLE)
      }
    }
  }
</script>
```

## 属性

<!-- prettier-ignore -->
| 属性名 | 类型 | 默认值 | 描述 |
| ------------------------ | ------- | --------- | ---------------------------------------------------------------------------------------------- |
| show | Boolean | `true` | `optional` 指定线是否可显示。 |
| positions | Array | | `optional` 指定表示线条的位置数组。 **结构：[{ lng: number, lat: number, height: number },...,{ lng: number, lat: number, height: number }]** |
| width | Number | `1.0` | `optional` 指定线的宽度（像素）。 |
| granularity | Number | | `optional` 指定每个经纬度之间的采样粒度。 arcType 不是 ArcType.NONE 时有效。 |
| material | Object\|String\|Array | `'WHITE'` | `optional` 指定用于绘制线的材质。 |
| depthFailMaterial | Object\|String\|Array | | `optional` 指定用于绘制低于地形的线的材质。 |
| arcType | Number | `1` | `optional` 指定线条类型。 **NONE: 0, GEODESIC: 1, RHUMB: 2** |
| clampToGround | Boolean | `false` | `optional` 指定线是否贴地。 |
| shadows | Number | | `optional` 指定这些是否投射或接收来自每个光源的阴影。 **DISABLED: 0, ENABLED: 1, CAST_ONLY: 2, RECEIVE_ONLY: 3, NUMBER_OF_SHADOW_MODES: 4, RECEIVE_ONLY: 3** |
| classificationType | Number | `2` | `optional` 指定相机到线的距离。 **TERRAIN: 0, CESIUM_3D_TILE: 1, BOTH: 2, NUMBER_OF_CLASSIFICATION_TYPES: 3** |
| distanceDisplayCondition | Object | | `optional` 指定相机到线的距离。 **结构：{ near: number, far: number }** |
| zIndex | Number | `0` | `optional` 指定用于排序地面几何的 zIndex。 仅当`clampToGround`为真且支持地形上的折线时才有效。 |

---

- 官方文档 [PolylineGraphics](https://cesiumjs.org/Cesium/Build/Documentation/PolylineGraphics.html)

## 事件

| 事件名            | 参数             | 描述                                                |
| ----------------- | ---------------- | --------------------------------------------------- |
| ready             | {Cesium, viewer} | 该组件渲染完毕时触发，返回 Cesium 类, viewer 实例。 |
| definitionChanged |                  | 每当更改或修改属性或子属性时触发该事件。            |
