<template>
  <div>
    <div
      ref="player"
      :style="{
        'max-width': '1000px',
        height: '200px',
        margin: '20px auto',
        border: 'dotted 10px green',
      }"
    />
  </div>
</template>

<script>
import Vue from 'vue'
import { createComponent, render } from 'solid-js/web'
import { SolidPlayer } from 'xsg-player-sdk'
import 'xsg-player-sdk/dist/style.css'
import 'xsg-player-sdk/fonts/stylesheet.css'
import { createSignal, mergeProps } from 'solid-js'

export default Vue.extend({
  data() {
    return {
      playerProps: {
        type: 'audio',
        autoPlay: true,
        muted: true,
        poster: 'https://picsum.photos/200',
        languages: [
          {
            label: 'GEO',
            qualities: [
              {
                label: '1080p',
                sources: [
                  {
                    src: 'https://ge.uploader.1tv.ge/1tvplay/1997-%E1%83%A5%E1%83%90%E1%83%A0%E1%83%97%E1%83%A3%E1%83%9A%E1%83%98-%E1%83%A1%E1%83%90%E1%83%97%E1%83%90%E1%83%A3%E1%83%A0%E1%83%98-3647d/647d8dd9f186f-1080p.mp4',
                  },
                ],
              },
              {
                label: '720p',
                sources: [
                  {
                    src: 'https://ge.uploader.1tv.ge/1tvplay/1997-%E1%83%A5%E1%83%90%E1%83%A0%E1%83%97%E1%83%A3%E1%83%9A%E1%83%98-%E1%83%A1%E1%83%90%E1%83%97%E1%83%90%E1%83%A3%E1%83%A0%E1%83%98-3647d/647d8f8e180db-720p.mp4',
                  },
                ],
              },
              {
                label: '480p',
                sources: [
                  {
                    src: 'https://ge.uploader.1tv.ge/1tvplay/1997-%E1%83%A5%E1%83%90%E1%83%A0%E1%83%97%E1%83%A3%E1%83%9A%E1%83%98-%E1%83%A1%E1%83%90%E1%83%97%E1%83%90%E1%83%A3%E1%83%A0%E1%83%98-3647d/647d90ef713fa-480p.mp4',
                  },
                ],
              },
            ],
          },
        ],
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
