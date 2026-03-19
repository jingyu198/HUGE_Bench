<script lang="ts" setup>
import { computed, ref } from 'vue'
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

const currentScene = computed(
  () => scenes.find((scene) => scene.key === selectedSceneKey.value) ?? scenes[0]
)
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
                    <VueCompareImage 
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
}
</style>
