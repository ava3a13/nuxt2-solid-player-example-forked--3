<template>
  <div
    :style="{
      display: 'flex',
      'flex-direction': 'column',
      gap: '16px',
    }"
  >
    <h2>Regular Audio Player</h2>
    <div ref="player" />
  </div>
</template>

<script>
import Vue from 'vue'
import { createComponent, render } from 'solid-js/web'
import { SolidPlayer } from 'xsg-player-sdk'
import 'xsg-player-sdk/dist/style.css'
import { createSignal, mergeProps } from 'solid-js'

export default Vue.extend({
  data() {
    return {
      playerProps: {
        type: 'audio',
        autoPlay: true,
        poster: 'https://picsum.photos/200',
        languages: [
          {
            label: 'GEO',
            qualities: [
              {
                label: '720p',
                sources: [
                  {
                    src: 'https://uploader.1tv.ge/1tvplay/demo/demo.mp3',
                  },
                ],
              },
            ],
          },
        ],
        onFinished: () => console.log('finished'),
      },
    }
  },
  mounted() {
    const [solidProps, setSolidProps] = createSignal(this.playerProps)

    this.$watch('playerProps', function (newProps) {
      setSolidProps(newProps)
    })

    return render(
      () => createComponent(SolidPlayer, mergeProps(solidProps)),
      this.$refs.player
    )
  },
})
</script>
