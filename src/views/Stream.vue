<template>
  <section class="stream">
    <button @click="stopStream" v-if="streaming">Stop streaming</button>
    <video ref="video" autoplay></video>
  </section>
</template>

<script>
import { uniqueNamesGenerator, adjectives } from 'unique-names-generator'

const xmas = ['dog', 'puppy', 'pup', 'doggo', 'doge', 'cat', 'mouse']

const config = {
  dictionaries: [adjectives, xmas],
  separator: '-',
  length: 2,
  style: 'lowerCase'
}

const generateStreamName = () => uniqueNamesGenerator(config)

const videoConstraint = { audio: false, video: { width: 1280, height: 720 } }

export default {
  name: 'stream',
  data () {
    return {
      streaming: false,
      mediaStream: null,
      name: this.slug === 'new' ? generateStreamName() : this.slug
    }
  },
  props: {
    slug: String
  },
  created () {
    if (this.slug === 'new') return this.generateStream()

    this.getStream(this.slug)
  },
  methods: {
    async generateStream () {
      try {
        const stream = await navigator.mediaDevices.getUserMedia(videoConstraint)
        this.$refs.video.srcObject = stream
        this.streaming = true
        this.mediaStream = stream
        // TODO: Open WebSocket and send stream
      } catch (error) {
        alert(`${error.name}`)
        console.error(error)
      }
    },
    async getStream () {
      // TODO: Open WebSocket and get stream
    },
    async stopStream () {
      this.mediaStream.getTracks().forEach(track => track.stop())
      // TODO: Close WebSocket and terminate stream
      this.$router.push('/')
    }
  }
}
</script>
