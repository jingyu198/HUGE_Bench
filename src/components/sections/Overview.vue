<script setup>
import overviewImage from '../../../my_eccv/overview.png'
</script>

<template>
  <div class="overview-section">
    <el-row justify="center">
      <el-col :xs="22" :sm="20" :md="18" :lg="16" :xl="14">
        <div class="overview-image-wrap">
          <el-image :src="overviewImage" fit="contain" class="overview-image" />
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.overview-section {
  margin: 20px 0 8px;
}

.overview-image-wrap {
  display: flex;
  justify-content: center;
}

.overview-image {
  width: 100%;
  max-width: 960px;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}
</style>
