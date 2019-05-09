<template>
  <div class="red-package-contain">
    <img
      src="../assets/hongbao.png"
      :class="getClass()"
      :style="getStyle()"
      v-for="item in count"
      :key="item"
      @webkitAnimationStart="iterationStart(item, $event)"
      @webkitAnimationIteration="iterationEvent(item, $event)"
      @webkitAnimationend="Animationend(item, $event)"
    >
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    count: {
      type: Number,
      default: 30
    },
    minSize: {
      type: Number,
      default: 30
    },
    maxSize: {
      type: Number,
      default: 100
    }
  },
  data () {
    return {}
  },
  methods: {
    iterationStart (item, $event) {
      console.log('动画开始' + item)
    },
    iterationEvent (item, $event) {
      console.log('重复动画开始' + item)
      $event.target.style.cssText = this.getStyle()
    },
    Animationend (item, $event) {
      console.log('动画结束' + item)
    },
    getClass () {
      return `hb-item hbsd-${Math.floor(Math.random() * 50 + 30)}`
    },
    getStyle () {
      return `width:${Math.random() * (this.maxSize - this.minSize) +
        this.minSize}px;left:${Math.random() * 74 + 10}%`
    }
  }
}
</script>

<style lang="scss" scoped>
*{margin: 0;padding: 0;}
.red-package-contain {
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.hb-item {
  position: absolute;
  top: 0;
  z-index: 30000;
  cursor: pointer;
}
@keyframes startHB {
  0% {
    transform: translateY(-300px);
    -ms-transform: translateY(-300px);
    -webkit-transform: translateY(-300px);
  }
  100% {
    transform: translateY(100vh);
    -ms-transform: translateY(100vh);
    -webkit-transform: translateY(100vh);
  }
}
@keyframes chandou {
  0% {
    margin-left: -120px;
  }
  50% {
    margin-left: 0px;
  }
  100% {
    margin-left: 120px;
  }
}

$total: 100;
@for $i from 1 through $total {
  .hbsd-#{$i} {
    animation: startHB #{$i/20}s linear infinite,
      chandou #{$i/20}s infinite linear alternate both;
    -ms-animation: startHB #{$i/20}s linear infinite,
      chandou #{$i/20}s infinite linear alternate both;
    -webkit-animation: startHB #{$i/20}s linear infinite,
      chandou #{$i/20}s infinite linear alternate both;
  }
}
</style>
