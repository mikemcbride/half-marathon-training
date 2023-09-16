<template lang="html">
  <div class="p-4 mb-4 md:mb-0 rounded border-2 border-transparent" :class="{'border-indigo active-day-bg': activeDay}">
    <div class="uppercase mb-2 text-xs font-normal">
      {{ date }}
    </div>
    <div class="font-semibold text-xl">{{ workout }}</div>
  </div>
</template>

<script>
import { format, isToday } from 'date-fns'

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
  },
  computed: {
    date() {
      return format(this.day, 'dd')
    },
    activeDay() {
      return isToday(this.day)
    }
  },
}
</script>

<style scoped>
.active-day-bg {
  background: rgba(178, 183, 255, 0.6)
}
</style>
