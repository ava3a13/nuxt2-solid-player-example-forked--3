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
    <div
      :style="{
        margin: '20px',
      }"
    >
      <button
        @click="playPause"
        :style="{
          padding: '10px',
          border: '1px solid black',
          marginRight: '10px',
        }"
      >
        Play/Pause
      </button>
      <button
        @click="fastForward"
        :style="{
          padding: '10px',
          border: '1px solid black',
          marginRight: '10px',
        }"
      >
        FastForward
      </button>
      <button
        @click="rewind"
        :style="{
          padding: '10px',
          border: '1px solid black',
        }"
      >
        Rewind
      </button>
    </div>
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
                    src: 'https://uploader.1tv.ge/1tvplay/series/2021/1274/ge/64ff48a005b2e-1080p.mp4',
                  },
                ],
              },
              {
                label: '720p',
                sources: [
                  {
                    src: 'https://uploader.1tv.ge/1tvplay/series/2021/1274/ge/64ff53e88faee-720p.mp4',
                  },
                ],
              },
              {
                label: '480p',
                sources: [
                  {
                    src: 'https://uploader.1tv.ge/1tvplay/series/2021/1274/ge/64ff5d9256425-480p.mp4',
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
  methods: {
    playPause() {
      if (this.videoRef?.isPlaying()) {
        this.videoRef?.pause()
      } else {
        this.videoRef?.play()
      }
    },
    fastForward() {
      this.videoRef?.fastForward()
    },
    rewind() {
      this.videoRef?.rewind()
    },
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
