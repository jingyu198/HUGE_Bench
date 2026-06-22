<script>
import Title from './sections/Title.vue'
import Overview from './sections/Overview.vue'
import Abstract from './sections/Abstract.vue'
import InstructionVideos from './sections/InstructionVideos.vue'
import ImageSliderInner from './sections/ImageSliderInner.vue'
import TaskPipeline from './sections/TaskPipeline.vue'
import ResultsSection from './sections/ResultsSection.vue'
import RealToSim from './sections/RealToSim.vue'
import MoreVisualization from './sections/MoreVisualization.vue'
import PlatformVideo from './sections/PlatformVideo.vue'

export default {
  components: {
    Title,
    Overview,
    Abstract,
    InstructionVideos,
    ImageSliderInner,
    TaskPipeline,
    ResultsSection,
    RealToSim,
    MoreVisualization,
    PlatformVideo
  }
}
</script>

<template>
  <div class="main-sections">
    <Title/>
    <Overview/>
    <Abstract/>
    <MoreVisualization/>
    <ImageSliderInner/>
    <TaskPipeline/>
    <ResultsSection/>
    <RealToSim/>
    <PlatformVideo/>
    <InstructionVideos/>
  </div>
</template>

<style scoped>
.main-sections {
  display: flex;
  flex-direction: column;
  gap: 56px;
}

@media (max-width: 700px) {
  .main-sections {
    gap: 40px;
  }
}
</style>
