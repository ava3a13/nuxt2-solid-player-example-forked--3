<template>
  <div>
    <AudioPlayer />
    <SolidPlayer />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import SolidPlayer from '~/components/SolidPlayer.vue'
import AudioPlayer from '~/components/AudioPlayer.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: { SolidPlayer, AudioPlayer },
})
</script>
