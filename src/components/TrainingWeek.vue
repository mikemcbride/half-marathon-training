<template>
  <div
    class="grid grid-cols-7 bg-gray-200 gap-px border-b border-gray-300 text-center text-xs font-semibold leading-6 text-gray-700 lg:flex-none" :class="week === 11 && 'rounded-b-md'">
        <TrainingDay v-for="(day, index) in days" :key="index" :day="day" :workout="workouts[index]" :week="week" />
  </div>
</template>

<script>
import { subWeeks, addDays, format } from 'date-fns'
import TrainingDay from './TrainingDay.vue'

export default {
  name: 'TrainingWeek',
  components: {
    TrainingDay,
  },
  props: {
    workouts: {
      type: Array,
      required: true,
    },
    raceDay: {
      type: Date,
      required: true,
    },
    week: {
      type: Number,
      required: true,
    },
  },
  computed: {
    startDate() {
      const res = subWeeks(this.raceDay, 12 - this.week)
      return addDays(res, 1)
    },
    formattedStartDate() {
      return format(this.startDate, 'MMM d')
    },
    days() {
      return [0, 1, 2, 3, 4, 5, 6].map(i => addDays(this.startDate, i))
    },
  },
}
</script>
