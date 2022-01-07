<template>
  <h2>This is ContentA Page</h2>
  <Marquee :send-marquee='marquees'></Marquee>
  <Video></Video>
</template>

<script>
import Marquee from '@/components/Marquee.vue'
import Video from '@/components/Video.vue'
export default {
  inject: ['useWebsocket'],
  components: {
    Marquee,
    Video
  },
  props: {
    contentA: {
      type: Object,
      default () {
        return {
          uuid: ''
        }
      }
    }
  },
  data () {
    return {
      pageUUID: '',
      useWebSocket: null,
      messages: [],
      video: [],
      name: [],
      marquees: [],
      type: ''
    }
  },
  methods: {
    getFirstData () {
    },
    filterData (data) {
      this.messages.push(data)
      this.messages.forEach((item) => {
        this.type = item.type
        switch (this.type) {
          case 'marquee' :
            if (this.marquees.indexOf(item.source) === -1) {
              this.marquees.push(item.source)
            }
            console.log(this.marquees)
            break
          case 'youtube' :
            if (this.video.indexOf(item.source) === -1) {
              this.video.push(item.source)
            }
            console.log(this.video)
            break
        }
      })
    }
  },
  mounted () {
    this.pageUUID = this.$route.query.uuid

    this.useWebSocket = this.useWebsocket()
    this.useWebSocket.onopen = (e) => {
      console.log('onOpen', e)
      console.log('This is ContentA page 成功連線至 WebSocket Server')
    }

    this.useWebSocket.onmessage = (e) => {
      console.log('this is onmessage')
      const obj = JSON.parse(e.data)
      this.filterData(obj)
    }
  }
}
</script>
