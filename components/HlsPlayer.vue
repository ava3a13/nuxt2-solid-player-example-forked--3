<template>
  <div>
    <div
      ref="player"
      :style="{
        //'max-width': '1000px',
        //'aspect-ratio': '16/9',
        margin: '20px auto',
        border: 'dotted 10px green',
        //overflow: 'hidden',
      }"
    />
  </div>
</template>

<script>
import Vue from 'vue'
import { createComponent, render } from 'solid-js/web'
import { SolidPlayer } from 'xsg-player-sdk'
import 'xsg-player-sdk/dist/style.css'
//import 'xsg-player-sdk/fonts/stylesheet.css'
import { createSignal, mergeProps } from 'solid-js'

export default Vue.extend({
  data() {
    return {
      videoRef: null,
      playerProps: {
        hls: true,
        autoPlay: true,
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
              }
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
