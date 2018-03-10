<template>
  <div class="hello">
    <el-slider
      v-model="range"
      range
      :max="303"
      show-tooltip
      :format-tooltip="format"
      @change="renderAudio"
    >
    </el-slider>
    <button @click="play">Play</button>
    <button @click="pause">Pause</button>
  </div>
</template>

<script>
import {Howl} from 'howler'

export default {
  name: 'HelloWorld',
  data () {
    return {
      src: ['/static/audio.mp3'],
      sound: null,
      range: [0, 100]
    }
  },
  created () {
    this.sound = new Howl({
      src: this.src,
      sprite: {
        ring: [8000, 7000, true]
      }
    })
  },
  methods: {
    renderAudio (value) {
      this.sound.pause()

      console.log(value, this.range)
      this.sound = new Howl({
        src: this.src,
        sprite: {
          ring: [this.range[0] * 1000, this.range[1] * 1000, true]
        }
      })

      this.sound.play('ring')
    },
    format (value) {
      return value
    },
    play () {
      this.sound.play('ring')
    },
    pause () {
      this.sound.pause()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
  .hello {
    margin: auto;
    width: 500px;
  }
</style>
