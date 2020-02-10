<template>
  <time class="time" :datetime="date" :title="date">
    {{ timeAgo }}
  </time>
</template>

<script>
const units = [
  ['year', 31536000],
  ['month', 2592000],
  ['day', 86400],
  ['hour', 3600],
  ['minute', 60],
  ['second', 1]
]

// Based on https://gist.github.com/mage3k/e4b0eb24d4a19b28f4f24aee8a194107
const duration = (timeAgoInSeconds) => {
  for (let [name, seconds] of units) {
    const interval = Math.floor(timeAgoInSeconds / seconds)

    if (interval >= 1) {
      return {
        interval: interval,
        unit: name
      }
    }
  }
}

export default {
  name: 'Timestamp',
  data () {
    return {
      now: new Date(),
      timer: null
    }
  },
  mounted () {
    if (this.secondsAgo < this.timeLimit)
      this.timer = setInterval(() => { this.now = new Date() }, this.interval)
  },
  beforeDestroy () {
    if (this.timer) clearInterval(this.timer)
  },
  props: {
    timeLimit: {
      type: Number,
      default: 3600
    },
    interval: {
      type: Number,
      default: 5000
    },
    date: {
      type: Date,
      default: new Date()
    }
  },
  computed: {
    secondsAgo () {
      return Math.floor((this.now - this.date) / 1000)
    },
    timeAgo () {
      if (this.secondsAgo == 0)
        return 'just now'

      const { interval, unit } = duration(this.secondsAgo)
      const suffix = interval === 1 ? '' : 's'

      return `${interval} ${unit}${suffix} ago`
    }
  }
}
</script>

<style scoped>
.time {
  padding: 1rem;
  font-weight: normal;
  font-style: italic;
}
</style>
