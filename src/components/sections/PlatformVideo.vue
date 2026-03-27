<script setup>
import platformVideo from '../../../my_eccv/platform.mp4'
</script>

<template>
  <section class="platform-video-section">
    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="16" :xl="14">
        <video
          class="platform-video"
          :src="platformVideo"
          controls
          playsinline
          preload="metadata"
        />
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.platform-video-section {
  margin: 0 0 12px;
}

.platform-video {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  background: #000;
}
</style>
