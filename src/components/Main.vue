<script>
import Title from './sections/Title.vue'
import Overview from './sections/Overview.vue'
import Abstract from './sections/Abstract.vue'
import InstructionVideos from './sections/InstructionVideos.vue'
import BibTeX from './sections/BibTeX.vue'
import ImageSliderInner from './sections/ImageSliderInner.vue'
import ImageSelector from './sections/ImageSelector.vue'
import Model3D from './sections/Model3D.vue'
import GaussianSplats3D from './sections/GaussianSplats3D.vue'

export default {
  components: {
    Title,
    Overview,
    Abstract,
    InstructionVideos,
    BibTeX,
    ImageSliderInner,
    ImageSelector,
    Model3D,
    GaussianSplats3D
  }
}
</script>

<template>
  <Title/>
  <Overview/>
  <Abstract/>
  <InstructionVideos/>
  <Model3D/>
  <GaussianSplats3D/>
  <ImageSliderInner/>
  <ImageSelector/>
  <BibTeX/>
</template>
