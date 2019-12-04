<template>
  <section class="stream">
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
        // TODO: Open WebSocket and send stream
      } catch (error) {
        alert(`${error.name}`)
        console.error(error)
      }
    },
    async getStream () {
      // TODO: open WebSocket and get stream
    }
  }
}
</script>
