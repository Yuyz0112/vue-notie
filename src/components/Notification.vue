<template>
  <div class="notification fixed"
  v-if="show"
  :style="setStyle"
  transition="slide">
    <div class="delete"
    v-if="!options.autoClose"
    @click="close()"></div>
    <div class="content">
      {{{ options.content }}}
    </div>
  </div>
  <div class="countdown"
  v-if="show && options.autoClose && options.countdownBar"
  :style="setTime"
  :class="barControl"></div>
</template>

<script>
export default {
  data () {
    return {
      timers: [],
      barControl: ''
    }
  },
  props: {
    options: {
      type: Object,
      default: () => {
        return {}
      }
    },
    show: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    setStyle () {
      return {
        color: this.options.textColor || '#fff',
        background: this.options.backgroundColor || '#21e7b6'
      }
    },
    setTime () {
      return {
        transition: `all ${(this.options.showTime / 1000) || 3}s linear`,
        background: this.options.barColor || '#03D6D2'
      }
    }
  },
  methods: {
    countdown () {
      if (this.options.autoClose) {
        if (this.options.countdownBar) {
          setTimeout(() => {
            this.barControl = 'count-leave'
          }, 10)
        }
        const t = setTimeout(() => {
          this.close()
        }, this.options.showTime || 3000)
        this.timers.push(t)
      }
    },
    close () {
      this.show = false
      this.options = {}
    }
  },
  watch: {
    options () {
      this.barControl = ''
      this.timers.forEach((timer) => {
        window.clearTimeout(timer)
      })
      this.timers = []
      this.countdown()
    }
  }
}
</script>

<style scoped lang="sass">
  .slide-transition
    transition: all .3s ease
    transform: translate3d(0, 0, 0)
  .slide-enter,
  .slide-leave
    transform: translate3d(0, -100%, 0)
  .delete
    -moz-appearance: none
    -webkit-appearance: none
    background: rgba(51,51,51,0.2)
    cursor: pointer
    display: inline-block
    height: 24px
    position: relative
    vertical-align: top
    width: 24px
    float: right
    &:before,
    &:after
      background: #fff
      content: ""
      display: block
      height: 2px
      left: 50%
      margin-left: -25%
      margin-top: -1px
      position: absolute
      top: 50%
      width: 50%
    &:before
      transform: rotate(45deg)
    &:after
      transform: rotate(-45deg)
    &:hover
      background: rgba(51,51,51,0.5)
  .notification
    width: 100%
    line-height: 2
    z-index: 3
    position: fixed
    top: 0
    left: 0
    .content
      padding: .75rem 2rem
  .countdown
    width: 100%
    height: 4px
    background: #000
    z-index: 3
    position: fixed
    top: 0
    left: 0
    transform: translate3d(0, 0, 0)
  .count-leave
    transform: translate3d(-100%, 0, 0)
</style>