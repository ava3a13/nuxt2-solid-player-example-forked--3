<template>
  <div>
    <div
      ref="player"
      :style="{
        //'max-width': '1000px',
        //height: '200px',
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
//import 'xsg-player-sdk/fonts/stylesheet.css'
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
                label: '720p',
                sources: [
                  {
                    src: 'https://ia804706.us.archive.org/18/items/abba-abba-gold-greatest-hits_202301/ABBA%20Gold-%20Greatest%20Hits/07%20I%20Have%20A%20Dream.mp3',
                  },
                ],
              },
              {
                label: '480p',
                sources: [
                  {
                    src: 'https://ia904706.us.archive.org/18/items/abba-abba-gold-greatest-hits_202301/ABBA%20Gold-%20Greatest%20Hits/09%20Money%2C%20Money%2C%20Money.mp3',
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
