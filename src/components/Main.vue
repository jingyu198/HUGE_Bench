<script>
import Title from './sections/Title.vue'
import Overview from './sections/Overview.vue'
import Abstract from './sections/Abstract.vue'
import InstructionVideos from './sections/InstructionVideos.vue'
import BibTeX from './sections/BibTeX.vue'
import ImageSliderInner from './sections/ImageSliderInner.vue'
import ImageSlider from './sections/ImageSlider.vue'
import TaskPipeline from './sections/TaskPipeline.vue'
import RealToSim from './sections/RealToSim.vue'
import ImageSelector from './sections/ImageSelector.vue'

export default {
  components: {
    Title,
    Overview,
    Abstract,
    InstructionVideos,
    BibTeX,
    ImageSliderInner,
    ImageSlider,
    TaskPipeline,
    RealToSim,
    ImageSelector
  }
}
</script>

<template>
  <Title/>
  <Overview/>
  <Abstract/>
  <InstructionVideos/>
  <ImageSliderInner/>
  <ImageSlider/>
  <TaskPipeline/>
  <RealToSim/>
  <ImageSelector/>
  <BibTeX/>
</template>
