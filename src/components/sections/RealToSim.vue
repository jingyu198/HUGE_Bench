<script setup>
import realImage from '../../../my_eccv/real.png'

const caption =
  'Overview and results of the real-to-sim and sim-to-sim comparison experiments. Top-left: the experimental pipeline. Models are trained using either real-world data (real2sim) or synthetic data (sim2sim), and then evaluated in a digital twin environment with multiple random initializations. Top-right: quantitative test results showing the trajectory coverage rate (TCR) across different models under both settings. Bottom: qualitative trajectory comparisons for several representative test cases (Case 1-4). For each case, the predicted trajectory is compared with the ground truth in both real-to-sim and sim-to-sim evaluations.'
</script>

<template>
  <section class="real-to-sim-section">
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Real-to-Sim Analysis</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="14" :xl="12">
        <div class="image-wrap">
          <img :src="realImage" alt="Real-to-Sim Analysis" class="analysis-image" />
        </div>
        <p class="section-caption">{{ caption }}</p>
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

</style>
