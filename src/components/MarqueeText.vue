<script>
import { h, defineComponent } from 'vue'

export default defineComponent({
  name: 'MarqueeText',
  props: {
    duration: {
      type: Number,
      default: 15
    },
    repeat: {
      type: Number,
      default: 2,
      validator(val) {
        return val > 0
      }
    },
    paused: {
      type: Boolean,
      default: false
    },
    reverse: {
      type: Boolean,
      default: false
    },
    vertical: {
      type: Boolean,
      default: false
    }
  },
  render() {
    const {
      duration, repeat, paused, reverse, vertical
    } = this

    return h('div', { class: this.$style.wrap }, [
      h('div', {
        class: [
          paused
            ? this.$style.paused
            : '',
          this.$style.content
        ]
      }, Array.from(
        { length: repeat },
        (_, i) => h('div', {
          key: i, // 确保每个子元素有唯一的 key
          class: vertical ? this.$style.textVertical : this.$style.text,
          style: {
            animationDuration: `${duration}s`,
            animationDirection: reverse ? 'reverse' : undefined
          }
        },
        this.$slots.default())
      ))
    ])
  }
})
</script>

<style module>
.wrap {
  overflow: hidden;
}

.content {
  width: 100000px;
}

.text {
  animation-name: animation;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  float: left;
}

.textVertical {
  animation-name: animation-vertical;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}

.paused .text {
  animation-play-state: paused
}

@keyframes animation {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-100%);
  }
}

@keyframes animation-vertical {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-100%);
  }
}
</style>
