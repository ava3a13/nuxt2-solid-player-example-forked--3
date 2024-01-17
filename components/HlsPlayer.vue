<template>
  <div
    :style="{
      display: 'flex',
      'flex-direction': 'column',
      gap: '16px',
    }"
  >
    <h2>HLS Player (can Chrome Cast when on the same Wi-Fi with a device)</h2>
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
      videoRef: null,
      playerProps: {
        hls: true,
        autoplay: true,
        chromeCast: true,
        type: 'video',
        ref: (el) => {
          this.videoRef = el
        },
        languages: [
          {
            label: 'GEO',
            qualities: [
              {
                label: '1080p',
                sources: [
                  {
                    src: 'https://tv.cdn.xsg.ge/gpb-1tv/index.m3u8',
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
