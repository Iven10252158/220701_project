<template>
    <div class="marquee mb-3">
        <ul class="marquee-content mb-0">
            <li v-for="item in sendMarquee" :key="item.uuid">
              <span>{{ item.source }}</span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  props: {
    sendMarquee: {
      type: Object
    }
  }
}
</script>

<style lang="scss" scoped>
.marquee {
  height: 40px;
  display: flex;
  align-items: center;
  overflow: hidden;
  position: relative;
  background: black;
}

.marquee-content {
  padding-left: 100%;
  display: flex;
  list-style: none;
  position: absolute;
  li {
    white-space: nowrap;
    margin-right: 2em;
    animation: marquee 10s linear infinite;
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
