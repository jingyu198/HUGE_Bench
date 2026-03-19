<script>
import Title from './sections/Title.vue'
import Overview from './sections/Overview.vue'
import Abstract from './sections/Abstract.vue'
import InstructionVideos from './sections/InstructionVideos.vue'
import BibTeX from './sections/BibTeX.vue'
import ImageSliderInner from './sections/ImageSliderInner.vue'
import TaskPipeline from './sections/TaskPipeline.vue'
import RealToSim from './sections/RealToSim.vue'

export default {
  components: {
    Title,
    Overview,
    Abstract,
    InstructionVideos,
    BibTeX,
    ImageSliderInner,
    TaskPipeline,
    RealToSim
  }
}
</script>

<template>
  <div class="main-sections">
    <Title/>
    <Overview/>
    <Abstract/>
    <InstructionVideos/>
    <ImageSliderInner/>
    <TaskPipeline/>
    <RealToSim/>
    <BibTeX/>
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
