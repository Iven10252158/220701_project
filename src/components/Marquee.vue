<template>
    <div class="marquee">
        <ul class="marquee-content-lightRail mb-0">
            <li v-for="item in innerMarquee" :key="item">
              <span>{{ item }}</span>
            </li>
        </ul>

        <ul class="marquee-content-station mb-0">
            <li>
              <span></span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  props: ['sendMarquee'],
  data () {
    return {
      innerMarquee: this.sendMarquee,
      content: [],
      name: []
    }
  },
  methods: {
    getMarquee () {
      // this.innerMarquee.forEach(item => {
      //   this.content = item
      // })
      console.log(this.innerMarquee)
    }
  },
  mounted () {
    this.getMarquee()
  }
}
</script>

<style lang="scss" scoped>
.marquee {
 height: 2em;
 margin: 0 auto;
 overflow: hidden;
 position: relative;
 background: black;
}

.marquee-content-lightRail {
  // padding-left: 0;
  display: flex;
  list-style: none;
  animation: marquee 40s linear infinite;
  position: absolute;
  li {
    white-space: nowrap;
    margin-right: 2em;
      span {
        font-weight: bold;
        color: yellow;
      }
  }
}

.marquee-content-station {
  // padding-left: 0;
  display: flex;
  list-style: none;
  animation: marquee 15s linear infinite;
  position: absolute;
  li {
    white-space: nowrap;
    margin-right: 2em;
      span {
        font-weight: bold;
        color: yellow;
      }
  }
}

@keyframes marquee {
  0% {
    left: 100%;
    transform: translateX(0%);
  }

  100% {
    left: 0;
    transform: translateX(-100%);
  }
}

</style>
