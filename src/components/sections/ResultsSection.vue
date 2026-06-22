<script setup>
import overallComparisonImage from '../../../my_eccv/more_findings/results_overall_comparison.png'
import perTaskNdtwImage from '../../../my_eccv/more_findings/results_per_task_ndtw.png'

const overallCaption =
  'Overall comparison on the test set. We report both process-oriented metrics and safety metrics across different baseline models. Gray values indicate limited comparative significance due to low performance, e.g., spinning in place.'

const perTaskCaption =
  'Per-task nDTW comparison on seen and unseen sets.'
</script>

<template>
  <section class="results-section">
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Results</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="16" :xl="14">
        <div class="results-grid">
          <article class="result-card">
            <div class="result-media">
              <img
                :src="overallComparisonImage"
                alt="Overall comparison on the test set"
                class="result-image"
              />
            </div>
            <p class="result-caption">{{ overallCaption }}</p>
          </article>

          <article class="result-card">
            <div class="result-media">
              <img
                :src="perTaskNdtwImage"
                alt="Per-task nDTW comparison on seen and unseen sets"
                class="result-image"
              />
            </div>
            <p class="result-caption">{{ perTaskCaption }}</p>
          </article>
        </div>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.results-section {
  margin-bottom: 12px;
}

.results-grid {
  margin-top: 20px;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 22px;
}

.result-card {
  padding: 18px;
  border-radius: 18px;
  background: #ffffff;
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.1);
}

.result-media {
  overflow: hidden;
  border-radius: 14px;
  background: #ffffff;
}

.result-image {
  width: 100%;
  display: block;
}

.result-caption {
  margin: 14px 0 0;
  font-size: 14px;
  line-height: 1.7;
}

@media (max-width: 800px) {
  .results-grid {
    grid-template-columns: 1fr;
  }
}
</style>
