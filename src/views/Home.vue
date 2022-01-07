<template>
    <ul class="list-unstyled outer mb-0">
      <li>
        <router-link :to="{path : 'contentA', query:{ uuid: uuid}}" class="text-decoration-none me-5">contentA</router-link>
      </li>
       <li>
        <router-link :to="{path : 'contentB', query:{ uuid: '5678'}}" class="text-decoration-none me-5">contentB</router-link>
      </li>
    </ul>
</template>
<script>
export default {
  data () {
    return {
      uuid: '',
      content: []
    }
  },
  methods: {
    getPageID () {
      const apiUrl = 'http://192.168.1.176:8080/template?clientid=acad41bb-0872-485b-9570-44ef0c8e9b3e'
      this.$http.get(apiUrl)
        .then(res => {
          console.log(res)
          this.uuid = res.data.id
          this.content = res.data.content
        })
    }
  },
  mounted () {
    this.getPageID()
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
