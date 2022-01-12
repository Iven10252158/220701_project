<template>
  <router-view v-if="isRouterAlive"/>
</template>

<script>
import { useWebsocket } from '@/configs/useWebsocket.js'
export default {
  data () {
    return {
      isRouterAlive: true
    }
  },
  provide () {
    return {
      useWebsocket,
      reload: this.reload
    }
  },
  methods: {
    reload () {
      this.isRouterAlive = false
      this.$nextTick(() => {
        this.isRouterAlive = true
      })
    }
  }
}

</script>

<style lang="scss">
  @import "./assets/all";
</style>
