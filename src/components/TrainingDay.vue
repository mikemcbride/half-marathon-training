<template lang="html">
  <div class="p-2 flex flex-col justify-between" :class="[inPast && !activeDay ? 'bg-gray-100 text-gray-400' : 'bg-white text-gray-700', activeDay ? 'border-2 border-blue-600' : '', dow === 0 && week === 11 && 'rounded-bl-md', dow === 6 && week === 11 && 'rounded-br-md']">
    <div class="flex justify-end mb-2 text-xs font-normal opacity-90">
      {{ date }}
    </div>
    <div class="font-medium text-sm">{{ workout }}</div>
  </div>
</template>

<script>
import { format, isPast, isToday, getDay } from 'date-fns'

export default {
  name: 'TrainingDay',
  props: {
    day: {
      type: Date,
      required: true,
    },
    workout: {
      type: String,
      required: true,
    },
    week: {
      type: Number,
      required: true,
    },
  },
  computed: {
    dow() {
      return getDay(this.day)
    },
    date() {
      let dom = format(this.day, 'd')
      let f = 'd'
      // first day of week and first day of month get formatted w/ month
      if (dom === '1' || this.dow === 1) {
        f = 'MMM d'
      }
      return format(this.day, f)
    },
    activeDay() {
      return isToday(this.day)
    },
    inPast() {
      return isPast(this.day)
    }
  },
}
</script>

<style scoped>
.active-day-bg {
  background: rgba(178, 183, 255, 0.6)
}
</style>
