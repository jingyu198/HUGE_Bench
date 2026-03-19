<script lang="ts" setup>
import { computed, onMounted, ref, watch } from 'vue'
import { VueCompareImage } from 'vue3-compare-image'
import scene1GsImage from '../../../my_eccv/render_compare_1/pose_000000_3dgs.png'
import scene1MeshImage from '../../../my_eccv/render_compare_1/pose_000000_mesh_flat.png'
import scene2GsImage from '../../../my_eccv/render_compare_2/pose_000000_3dgs.png'
import scene2MeshImage from '../../../my_eccv/render_compare_2/pose_000000_mesh_flat.png'
import scene3GsImage from '../../../my_eccv/render_compare_3/pose_000000_3dgs.png'
import scene3MeshImage from '../../../my_eccv/render_compare_3/pose_000000_mesh_flat.png'
import scene4GsImage from '../../../my_eccv/render_compare_4/pose_000000_3dgs.png'
import scene4MeshImage from '../../../my_eccv/render_compare_4/pose_000000_mesh_flat.png'

const scenes = [
  {
    key: 'scene-1',
    label: 'Scene 1',
    leftImage: scene1GsImage,
    rightImage: scene1MeshImage,
  },
  {
    key: 'scene-2',
    label: 'Scene 2',
    leftImage: scene2GsImage,
    rightImage: scene2MeshImage,
  },
  {
    key: 'scene-3',
    label: 'Scene 3',
    leftImage: scene3GsImage,
    rightImage: scene3MeshImage,
  },
  {
    key: 'scene-4',
    label: 'Scene 4',
    leftImage: scene4GsImage,
    rightImage: scene4MeshImage,
  },
]

const selectedSceneKey = ref(scenes[0].key)
const loadedSceneMap = ref(
  Object.fromEntries(scenes.map((scene) => [scene.key, false]))
)

const currentScene = computed(
  () => scenes.find((scene) => scene.key === selectedSceneKey.value) ?? scenes[0]
)

const currentSceneLoaded = computed(
  () => loadedSceneMap.value[currentScene.value.key]
)

const preloadImage = (src: string) =>
  new Promise<void>((resolve) => {
    const image = new Image()
    image.onload = () => resolve()
    image.onerror = () => resolve()
    image.src = src
  })

const preloadScene = async (scene: (typeof scenes)[number]) => {
  if (!scene || loadedSceneMap.value[scene.key]) {
    return
  }

  await Promise.all([
    preloadImage(scene.leftImage),
    preloadImage(scene.rightImage),
  ])

  loadedSceneMap.value = {
    ...loadedSceneMap.value,
    [scene.key]: true,
  }
}

const preloadRemainingScenes = async () => {
  for (const scene of scenes.slice(1)) {
    await preloadScene(scene)
  }
}

watch(selectedSceneKey, async (sceneKey) => {
  const selectedScene = scenes.find((scene) => scene.key === sceneKey)
  if (selectedScene) {
    await preloadScene(selectedScene)
  }
}, { immediate: true })

onMounted(() => {
  window.setTimeout(() => {
    preloadRemainingScenes()
  }, 400)
})
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">4 Real-World Digital Twin Scenes</h1>
    </el-row>

    <el-row justify="center">
        <el-col :xs="24" :sm="22" :md="20" :lg="18" :xl="18">
            <el-row justify="center" style="margin-top: 20px;">
              <el-radio-group v-model="selectedSceneKey" size="large" class="scene-switcher">
                <el-radio-button
                  v-for="scene in scenes"
                  :key="scene.key"
                  :label="scene.key"
                >
                  {{ scene.label }}
                </el-radio-button>
              </el-radio-group>
            </el-row>

            <el-row style="margin-top: 20px;" >
                <div class="compare-layout">
                  <span class="compare-label compare-label-left">3dgs</span>
                  <div class="compare-view">
                    <div v-if="!currentSceneLoaded" class="compare-loading">
                      Loading {{ currentScene.label }}...
                    </div>
                    <VueCompareImage 
                        v-else
                        :key="selectedSceneKey"
                        :left-image="currentScene.leftImage" 
                        :right-image="currentScene.rightImage"
                        :hover="true"
                    />
                  </div>
                  <span class="compare-label compare-label-right">mesh</span>
                </div>
            </el-row>
        </el-col>
    </el-row>

  </div>
</template>

<style scoped>
.scene-switcher {
  max-width: 100%;
}

.compare-layout {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 16px;
}

.compare-view {
  flex: 1;
}

.compare-loading {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 420px;
  border-radius: 12px;
  background: #f5f7fa;
  color: #606266;
  font-size: 16px;
  font-weight: 500;
}

.compare-label {
  width: 68px;
  font-size: 15px;
  font-weight: 600;
  text-align: center;
}

@media (max-width: 700px) {
  .compare-layout {
    gap: 10px;
  }

  .compare-label {
    width: 52px;
    font-size: 13px;
  }

  .compare-loading {
    min-height: 260px;
    font-size: 14px;
  }
}
</style>
