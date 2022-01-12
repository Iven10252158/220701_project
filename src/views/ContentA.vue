<template>
  <h2>This is ContentA Page</h2>
  <Marquee v-if="marquees.length !== 0" :send-marquee="marquees"></Marquee>
  <Video :send-video="videos"></Video>
  <button type="button" class="btn btn-primary btn-sm my-2" @click.prevent="reloadPage">重新整理</button>
    <div class="oexpo">
      <iframe v-if="isIframeAlive" width="100%" height="800" src="https://www.oexpo.io/vb/61402dde56663ed090deccf6" frameborder="0"></iframe>
    </div>
  <Image :send-image="images"></Image>
</template>

<script>
import Marquee from '@/components/Marquee.vue'
import Video from '@/components/Video.vue'
import Image from '@/components/Image.vue'
export default {
  inject: ['useWebsocket'],
  components: {
    Marquee,
    Video,
    Image
  },
  props: {
    contentA: {
      type: Object,
      default () {
        return {
          uuid: ''
        }
      }
    },
    autoplay: {
      type: Number,
      default: 1
    }
  },
  data () {
    return {
      isIframeAlive: true,
      pageUUID: '',
      player: null,
      useWebSocket: null,
      messages: [], // 接收所有的資料
      type: '', // 類別
      videos: [], // 所有影片的資料
      marquees: [], // 所有跑馬燈資料
      images: [], // 所有圖片的資料
      kukuclocks: [], // 所有咕咕鐘的資料
      intervalId: null // data 定義一個定時器id
    }
  },
  methods: {
    reloadPage () {
      console.log('iframe重整')
      this.isIframeAlive = false
      this.$nextTick(() => {
        this.isIframeAlive = true
      })
    },
    onEnded () {
      this.player.seekTo(0)
      console.log('## OnEnded')
    },
    getFirstData () {
      const apiUrl = 'http://192.168.1.176:8080/template?clientid=acad41bb-0872-485b-9570-44ef0c8e9b3e'
      this.$http.get(apiUrl)
        .then(res => {
          console.log(res)
          this.content = res.data.content
        })
    },
    filterData (data) {
      this.messages.push(data)
      this.messages.forEach(item => {
        this.type = item.type
        switch (this.type) {
          case 'marquee' :
            this.marquees.unshift(item)
            if (this.marquees.length === 2) {
              this.marquees.pop()
            }
            break
          case 'youtube' :
            this.videos.unshift(item)
            if (this.videos.length === 2) {
              this.videos.pop()
            }
            // console.log('youtube', item.source)
            break
          case 'kukuclock' :
            this.videos.unshift(item)
            if (this.videos.length >= 2) {
              this.videos.pop()
            }
            // console.log('kukuclock', item.source)
            break
          case 'image' :
            this.images.unshift(item)
            if (this.images.length === 2) {
              this.images.pop()
            }
            console.log(item.source)
            break
        }
      })
      console.log('marquees', this.marquees)
      console.log('image', this.images)
    }
  },
  mounted () {
    this.pageUUID = this.$route.query.uuid
    this.getFirstData()
    this.useWebSocket = this.useWebsocket()
    this.useWebSocket.onopen = (e) => {
      console.log('onOpen', e)
      console.log('This is ContentA page 成功連線至 WebSocket Server')
    }

    this.useWebSocket.onmessage = (e) => {
      console.log('1. this is onmessage')
      const obj = JSON.parse(e.data)
      this.filterData(obj)
    }
  }
}
</script>
