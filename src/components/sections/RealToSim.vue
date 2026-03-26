<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import realImage from '../../../my_eccv/real.png'
import platformVideo from '../../../my_eccv/platform.mp4'
import trajRealVideo from '../../../my_eccv/traj_real.mp4'
import trajSimVideo from '../../../my_eccv/traj_sim.mp4'

const caption =
  'Overview and results of the real-to-sim and sim-to-sim comparison experiments. Top-left: the experimental pipeline. Models are trained using either real-world data (real2sim) or synthetic data (sim2sim), and then evaluated in a digital twin environment with multiple random initializations. Top-right: quantitative test results showing the trajectory coverage rate (TCR) across different models under both settings. Bottom: qualitative trajectory comparisons for several representative test cases, with all results obtained from models trained on <i>&pi;</i><sub>0</sub>. For each case, the predicted trajectory is compared with the ground truth in both real-to-sim and sim-to-sim evaluations.'

const realVideoRef = ref(null)
const simVideoRef = ref(null)

let isSyncing = false
const removeListeners = []

const syncCurrentTime = (source, target) => {
  if (!source || !target || isSyncing) {
    return
  }

  if (Math.abs(source.currentTime - target.currentTime) < 0.08) {
    return
  }

  isSyncing = true
  target.currentTime = source.currentTime
  isSyncing = false
}

const syncPlayback = async (source, target) => {
  if (!source || !target || isSyncing) {
    return
  }

  isSyncing = true

  try {
    target.currentTime = source.currentTime
    if (target.paused || target.ended) {
      await target.play()
    }
  } catch (error) {
    console.warn('Unable to sync video playback.', error)
  } finally {
    isSyncing = false
  }
}

const syncPause = (target) => {
  if (!target || isSyncing) {
    return
  }

  isSyncing = true
  target.pause()
  isSyncing = false
}

const syncRate = (source, target) => {
  if (!source || !target || isSyncing) {
    return
  }

  isSyncing = true
  target.playbackRate = source.playbackRate
  isSyncing = false
}

const bindVideoSync = (source, target) => {
  if (!source || !target) {
    return
  }

  const listeners = [
    ['play', () => syncPlayback(source, target)],
    ['pause', () => syncPause(target)],
    ['seeking', () => syncCurrentTime(source, target)],
    ['ratechange', () => syncRate(source, target)],
  ]

  listeners.forEach(([eventName, handler]) => {
    source.addEventListener(eventName, handler)
    removeListeners.push(() => source.removeEventListener(eventName, handler))
  })
}

onMounted(() => {
  bindVideoSync(realVideoRef.value, simVideoRef.value)
  bindVideoSync(simVideoRef.value, realVideoRef.value)
})

onBeforeUnmount(() => {
  removeListeners.forEach((remove) => remove())
})
</script>

<template>
  <section class="real-to-sim-section">
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Data Collection Platform</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="14" :xl="12">
        <div class="platform-video-wrap">
          <video
            class="platform-video"
            :src="platformVideo"
            controls
            playsinline
            preload="metadata"
          />
        </div>
      </el-col>
    </el-row>

    <el-row justify="center">
      <h1 class="section-title">Real-to-Sim Analysis</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="14" :xl="12">
        <div class="image-wrap">
          <img :src="realImage" alt="Real-to-Sim Analysis" class="analysis-image" />
        </div>
        <p class="section-caption" v-html="caption"></p>

        <div class="video-comparison">
          <article class="video-card">
            <p class="video-label">Real-World Data</p>
            <video
              ref="realVideoRef"
              class="comparison-video"
              :src="trajRealVideo"
              controls
              playsinline
              preload="metadata"
            />
          </article>

          <article class="video-card">
            <p class="video-label">Synthetic Data</p>
            <video
              ref="simVideoRef"
              class="comparison-video"
              :src="trajSimVideo"
              controls
              playsinline
              preload="metadata"
            />
          </article>
        </div>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.real-to-sim-section {
  margin-bottom: 12px;
}

.image-wrap {
  margin-top: 20px;
}

.platform-video-wrap {
  margin-top: 20px;
  margin-bottom: 34px;
}

.platform-video {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  background: #000;
}

.analysis-image {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}

.section-caption {
  margin-top: 14px;
  font-size: 15px;
  line-height: 1.7;
}

.video-comparison {
  margin-top: 28px;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 20px;
}

.video-card {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.video-label {
  margin: 0;
  font-size: 15px;
  font-weight: 600;
  text-align: center;
}

.comparison-video {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  background: #000;
}

@media (max-width: 700px) {
  .video-comparison {
    grid-template-columns: 1fr;
  }
}

</style>
