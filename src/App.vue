<template>
  <router-view/>
</template>

<script>
import { useWebsocket } from '@/configs/useWebsocket.js'
export default {
  provide () {
    return {
      useWebsocket
    }
  }
}

</script>

<style lang="scss">
  @import "./assets/all";
</style>
