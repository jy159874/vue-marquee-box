<script>
import { h } from 'vue'

export default {
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
  render({
    $slots, $style, $props: {
      duration, repeat, paused, reverse, vertical
    }
  }) {
    return h('div', { class: [$style.wrap] }, [
      h('div', {
        class: [
          paused
            ? $style.paused
            : undefined,
          $style.content
        ]
      }, Array(repeat).fill(
        h('div', {
          class: vertical ? $style.textVertical : $style.text,
          style: {
            animationDuration: `${duration}s`,
            animationDirection: reverse
              ? 'reverse'
              : undefined
          }
        }, $slots.default())
      ))
    ])
  }
}
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
  0% { transform:translateX(0); }
  100% { transform:translateX(-100%); }
}

@keyframes animation-vertical {
  0% { transform:translateY(0); }
  100% { transform:translateY(-100%); }
}
</style>
