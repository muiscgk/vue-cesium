# 模型

`model-graphics` 模型组件，作为`entity`的子组件添加包含模型的实体到场景。基于 glTF 的 3D 模型。 模型的位置和方向由包含实体确定。Cesium 包括对 glTF 几何，材质，动画和蒙皮的支持。 目前不支持相机和灯光。如示例所示。

## 示例

### 添加模型到场景

#### 预览

<doc-preview>
  <template>
    <div class="viewer">
      <cesium-viewer @ready="ready">
        <entity :position="position1" :description="description" :model.sync="model1" :label.sync="label1">
          <label-graphics text="Hello Vue Cesium" font="20px sans-serif"></label-graphics>
          <model-graphics :uri="uri1" @ready="subReady"></model-graphics>
        </entity>
      </cesium-viewer>
    </div>
  </template>

  <script>
    export default {
      data() {
        return {
          description: 'Hello Vue Cesium',
          model1: {},
          label1: {},
          position1: { lng: 114.0, lat: 40.0, height: 1.0 },
          uri1: '/statics/SampleData/models/GroundVehicle/GroundVehicle.glb'
        }
      },
      methods: {
        ready(cesiumInstance) {
          const { Cesium, viewer } = cesiumInstance
        },
        subReady(cesiumInstance) {
          const { Cesium, viewer } = cesiumInstance
          viewer.zoomTo(viewer.entities)
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
      <entity :position="position1" :description="description" :model.sync="model1" :label.sync="label1">
        <label-graphics text="Hello Vue Cesium" font="20px sans-serif"></label-graphics>
        <model-graphics :uri="uri1" @ready="subReady"></model-graphics>
      </entity>
    </cesium-viewer>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        description: 'Hello Vue Cesium',
        model1: {},
        label1: {},
        position1: { lng: 114.0, lat: 40.0, height: 1.0 },
        uri1: '/statics/SampleData/models/GroundVehicle/GroundVehicle.glb'
      }
    },
    methods: {
      ready(cesiumInstance) {
        const { Cesium, viewer } = cesiumInstance
      },
      subReady(cesiumInstance) {
        const { Cesium, viewer } = cesiumInstance
        viewer.zoomTo(viewer.entities)
      }
    }
  }
</script>
```

## 属性

<!-- prettier-ignore -->
| 属性名 | 类型 | 默认值 | 描述 |
| ------------------------- | --------------------- | --------- | -------------------------------------------------------------------------------------------- |
| show | Boolean | `true` | `optional` 指定 model 是否显示。 |
| uri | String | | `optional` 指定 model 的 url 地址。 |
| scale | Number | `1.0` | `optional` 指定 model 缩放比例。 |
| minimumPixelSize | Number | `0.0` | `optional` 指定 model 的最小像素。 |
| maximumScale | Number | | `optional` 指定 model 最大像素。 |
| incrementallyLoadTextures | Boolean | `true` | `optional` 指定在加载模型后纹理是否可以继续流入。 |
| runAnimations | Boolean | `true` | `optional` 指定是否启动模型中的动画。 |
| clampAnimations | Boolean | `true` | `optional` 指定动画在没有帧动画的时候保持最后一个姿势。 |
| shadows | Number | `1` | `optional` 指定 model 是否投射或接收每个光源的阴影。 **DISABLED: 0, ENABLED: 1, CAST_ONLY: 2, RECEIVE_ONLY: 3, NUMBER_OF_SHADOW_MODES: 4, RECEIVE_ONLY: 3** |
| heightReference | Number | `0` | `optional` 指定 model 的高度模式。 **NONE: 0, CLAMP_TO_GROUND: 1, RELATIVE_TO_GROUND: 2** |
| silhouetteColor | Object\|String\|Array | `'RED'` | `optional` 指定 model 轮廓线颜色。 |
| silhouetteSize | Number | `0.0` | `optional` 指定 model 轮廓线像素尺寸。 |
| color | Object\|String\|Array | `'WHITE'` | `optional` 指定 model 渲染混合的颜色。 |
| colorBlendMode | Number | `0` | `optional` 指定 model 与颜色混合模式。 **HIGHLIGHT: 0, REPLACE: 1, MIX: 2** |
| colorBlendAmount | Number | `0.5` | `optional` 指定 colorBlendMode 为 MIX 的颜色强度。0 表示模型颜色，1 表示纯色，0-1 表示混合。 |
| imageBasedLightingFactor | Object | `{x: 1.0, y: 1.0}` | `optional` 指定漫反射和镜面反射因子。 |
| lightColor | Object\|String\|Array | | `optional` 指定着色模型时要使用的灯光颜色的属性。未指定是太阳颜色。 |
| distanceDisplayCondition | Object | | `optional` 指定模型随相机改变的显示条件。 **结构：{ near: number, far: number }** |
| nodeTransformations | Object | | `optional` 设置 TranslationRotationScale 节点转换参数。**结构：{translation: {x: number, y: number, z: number}, rotation: {x: number, y: number, z: number, w: number}, scale:{x: number, y: number, z: number}}** |
| articulations | Object | | `optional` |
| clippingPlanes | Object | | `optional` 指定模型屏幕裁剪参数。 |

---

- 官方文档 [ModelGraphics](https://cesiumjs.org/Cesium/Build/Documentation/ModelGraphics.html)

## 事件

| 事件名            | 参数             | 描述                                                |
| ----------------- | ---------------- | --------------------------------------------------- |
| ready             | {Cesium, viewer} | 该组件渲染完毕时触发，返回 Cesium 类, viewer 实例。 |
| definitionChanged |                  | 每当更改或修改属性或子属性时触发该事件。            |
