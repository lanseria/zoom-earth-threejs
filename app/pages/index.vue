<script setup lang="ts">
import { useTexture } from '@tresjs/core'

const { resume } = useRenderLoop()

// 加载多个材质贴图
const textureMap = await useTexture({
  map: '/textures/earth2.png', // 基础颜色贴图
})

onMounted(() => {
  resume()
})
</script>

<template>
  <div>
    <TresCanvas
      :window-size="true"
      clear-color="#181D1B"
    >
      <TresPerspectiveCamera :position="[3, 3, 3]" />
      <OrbitControls />

      <!-- 球体对象 -->
      <TresMesh>
        <TresSphereGeometry :args="[1, 64, 64]" />
        <TresMeshStandardMaterial
          :map="textureMap.map"
          :normal-map="textureMap.normalMap"
          :roughness-map="textureMap.roughnessMap"
          :roughness="0.7"
          :metalness="0.2"
        />
      </TresMesh>

      <!-- 照明系统 -->
      <TresAmbientLight :intensity="0.3" />
      <TresDirectionalLight
        :position="[5, 5, 5]"
        :intensity="2"
        cast-shadow
      />
    </TresCanvas>
  </div>
</template>
