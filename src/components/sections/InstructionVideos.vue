<script setup>
import instructionsText from '../../../my_eccv/instr.txt?raw'
import media1 from '../../../my_eccv/media1.mp4'
import media2 from '../../../my_eccv/media2.mp4'
import media3 from '../../../my_eccv/media3.mp4'
import media4 from '../../../my_eccv/media4.mp4'
import media5 from '../../../my_eccv/media5.mp4'
import media6 from '../../../my_eccv/media6.mp4'
import media7 from '../../../my_eccv/media7.mp4'
import media8 from '../../../my_eccv/media8.mp4'

const instructions = instructionsText
  .split(/\r?\n/)
  .map((line) => line.trim())
  .filter(Boolean)

const videoSources = [media1, media2, media3, media4, media5, media6, media7, media8]

const videos = videoSources.map((src, index) => ({
  src,
  title: instructions[index] || `Example ${index + 1}`,
  startTime: index === 2 ? 1.5 : 0,
}))

const applyStartTime = (event, startTime) => {
  if (!startTime) {
    return
  }

  const video = event.target
  video.currentTime = startTime
}
</script>

<template>
  <section class="instruction-videos">
    <el-row justify="center">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="18">
        <h2 class="section-title">High-Level VLA Trajectories in HUGE-Bench</h2>
        <div class="videos-grid">
          <article v-for="(video, index) in videos" :key="index" class="video-card">
            <h3 class="video-title">{{ video.title }}</h3>
            <video
              class="video-player"
              :src="video.src"
              controls
              playsinline
              preload="metadata"
              @loadedmetadata="applyStartTime($event, video.startTime)"
            />
          </article>
        </div>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.instruction-videos {
  margin: 28px 0 12px;
}

.section-title {
  margin: 0 0 24px;
  text-align: center;
}

.videos-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  column-gap: 20px;
  row-gap: 64px;
}

.video-card {
  display: flex;
  flex-direction: column;
  gap: 10px;
  height: 100%;
}

.video-title {
  margin: 0;
  font-size: 14px;
  font-weight: 400;
  line-height: 1.45;
  text-align: center;
}

.video-player {
  margin-top: auto;
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  background: #000;
}

@media (max-width: 1100px) {
  .videos-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 700px) {
  .videos-grid {
    grid-template-columns: 1fr;
  }
}
</style>
