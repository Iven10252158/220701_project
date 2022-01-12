
<template>
<swiper class="mySwiper"
  :loop="true"
  :pagination='{
    "type": "progressbar"
  }'
  :mousewheel="true"
  :autoplay='{ "delay": 2500, "disableOnInteraction": false }' >
  <swiper-slide v-for="item in sendImage" :key="item.source">
    <img class="swiper-img" :src="item.source" alt="">
    <!-- <div class="bg-cover" :style="{backgroundImage:'url(' +item.source+ ')'}"></div> -->
  </swiper-slide>
  </swiper>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue'

// Import Swiper styles
// swiper bundle styles
import 'swiper/swiper-bundle.min.css'

// swiper core styles
import 'swiper/swiper.min.css'

// modules styles
import 'swiper/components/navigation/navigation.min.css'
import 'swiper/components/pagination/pagination.min.css'

// import Swiper core and required modules
import SwiperCore, {
  Navigation, Pagination, Autoplay
} from 'swiper'

// install Swiper modules
SwiperCore.use([Navigation, Pagination, Autoplay])

export default {
  components: {
    Swiper,
    SwiperSlide
  },
  props: {
    sendImage: {
      type: Object
    }
  },
  data () {
    return {
    }
  },
  methods: {

  }

}
</script>
<style lang="scss" scoped>
    // .bg-cover{
    //   background-position: center center;
    //   background-size: cover;
    //   padding-top: 56.397%; //66.721%;
    // }
    .swiper-img{
      width: 100%;
      object-fit: cover;
      object-position: center center;
    }
</style>
