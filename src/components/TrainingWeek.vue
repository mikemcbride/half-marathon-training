<template lang="html">
  <div
    class="border-2 bg-white shadow rounded mb-4 p-6"
    :class="{
      'border-transparent': !isActiveWeek,
      'border-indigo': isActiveWeek,
      'opacity-50': isInPast,
    }"
  >
    <h3 class="mb-6">Week of {{ formattedStartDate }}</h3>
    <div class="flex flex-col md:flex-row justify-between">
      <TrainingDay
        v-for="(day, index) in days"
        :key="index"
        :day="day"
        :workout="workouts[index]"
      />
    </div>
  </div>
</template>

<script>
import subWeeks from 'date-fns/sub_weeks'
import addDays from 'date-fns/add_days'
import format from 'date-fns/format'
import isSameWeek from 'date-fns/is_same_week'
import isPast from 'date-fns/is_past'
import TrainingDay from '@/components/TrainingDay'

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
      return format(this.startDate, 'MMM D')
    },
    days() {
      return [0, 1, 2, 3, 4, 5, 6].map(i => addDays(this.startDate, i))
    },
    isActiveWeek() {
      let today = new Date()
      return isSameWeek(today, this.startDate)
    },
    isInPast() {
      if (this.isActiveWeek === true) {
        return false
      }

      return isPast(this.startDate)
    },
  },
}
</script>
