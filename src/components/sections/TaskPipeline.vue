<script setup>
import taskImage from '../../../my_eccv/task.png'
import pipelineImage from '../../../my_eccv/pipeline.png'

const figures = [
  {
    image: taskImage,
    alt: 'Task definition comparison',
    caption:
      'Difference between previous VLN tasks and HL-VLA tasks. Left: a VLN task example where the UAV follows a long-horizon navigation instruction through multiple landmarks. Right: a HL-VLA task example with a high-level instruction decomposed into temporally aligned subtasks for structured trajectory execution.',
  },
  {
    image: pipelineImage,
    alt: 'Trajectory generation pipeline',
    caption:
      'Trajectory generation pipeline of HUGE-Bench. Starting from real-world data collection, we reconstruct 3D environments using 3DGS and mesh representations. Landmarks are localized and annotated to generate spatial descriptions and task instructions. Trajectories are collected in the simulation platform with multimodal observations, including RGB, depth, 4-DoF state, and subtask phases.',
  },
]
</script>

<template>
  <section class="task-pipeline-section">
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Task Definition and Trajectory Generation Pipeline</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="14" :xl="12">
        <div class="figures-grid">
          <figure v-for="figure in figures" :key="figure.alt" class="figure-card">
            <img :src="figure.image" :alt="figure.alt" class="figure-image" />
            <figcaption class="figure-caption">{{ figure.caption }}</figcaption>
          </figure>
        </div>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.task-pipeline-section {
  margin-bottom: 12px;
}

.figures-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 40px;
  margin-top: 20px;
}

.figure-card {
  margin: 0;
}

.figure-image {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}

.figure-caption {
  margin-top: 14px;
  font-size: 15px;
  line-height: 1.7;
  text-align: justify;
}

</style>
