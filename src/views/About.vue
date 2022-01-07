<template>
    <h1>This is an about page</h1>
    <ul class="list-unstyled outer mb-0">
      <li>
        <router-link :to="{path : 'contentA', query:{ uuid: this.contentA_UUID}}" class="text-decoration-none me-5">contentA</router-link>
      </li>
       <li>
        <router-link :to="{path : 'contentB', query:{ uuid: this.contentB_UUID}}" class="text-decoration-none me-5">contentB</router-link>
      </li>
    </ul>
</template>

<script>
export default {
  inject: ['useWebsocket'],
  data () {
    return {
      connection: null,
      messages: [],
      contentA_UUID: '',
      contentB_UUID: ''
    }
  },

  methods: {

  },

  created () {
    console.log(this.useWebsocket())
    //   const connection = new WebSocket(WS_ADDRESS)
    this.connection = this.useWebsocket()
    //   this.connect()
    this.connection.onopen = (e) => {
      console.log('onOpen事件', e)
      console.log('已成功連線至 WebSocket Server')
    }

    this.connection.onmessage = (e) => {
      console.log('this is onmessage')
    }
  }
}
</script>

<style lang="scss" scoped>
  .outer {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: orange;
  }
</style>
