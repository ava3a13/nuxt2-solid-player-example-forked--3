<template>
  <div
    :style="{
      'max-width': '1000px',
      margin: '20px auto',
      display: 'flex',
      'flex-direction': 'column',
      gap: '32px',
    }"
  >
    <AudioPlayer />
    <SolidPlayer />
    <ExternalControls />
    <HlsPlayer />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import SolidPlayer from '~/components/SolidPlayer.vue'
import HlsPlayer from '~/components/HlsPlayer.vue'
import AudioPlayer from '~/components/AudioPlayer.vue'
import ExternalControls from '~/components/ExternalControls.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: { SolidPlayer, AudioPlayer, HlsPlayer, ExternalControls },
})
</script>
