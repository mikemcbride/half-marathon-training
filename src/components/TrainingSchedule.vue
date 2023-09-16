<template lang="html">
<div class="shadow ring-1 ring-black ring-opacity-5 lg:flex lg:flex-auto lg:flex-col rounded-md">
      <div class="grid grid-cols-7 gap-px border-b border-gray-300 bg-gray-200 text-center text-xs font-semibold leading-6 text-gray-700 lg:flex-none rounded-t-md">
        <div class="bg-white py-2 rounded-tl-md">S<span class="sr-only sm:not-sr-only">un</span></div>
        <div class="bg-white py-2">M<span class="sr-only sm:not-sr-only">on</span></div>
        <div class="bg-white py-2">T<span class="sr-only sm:not-sr-only">ue</span></div>
        <div class="bg-white py-2">W<span class="sr-only sm:not-sr-only">ed</span></div>
        <div class="bg-white py-2">T<span class="sr-only sm:not-sr-only">hu</span></div>
        <div class="bg-white py-2">F<span class="sr-only sm:not-sr-only">ri</span></div>
        <div class="bg-white py-2 rounded-tr-md">S<span class="sr-only sm:not-sr-only">at</span></div>
    </div>
    <TrainingWeek
      v-for="(workouts, $index) in schedule"
      :key="$index"
      :week="$index"
      :workouts="workouts"
      :race-day="raceDay"
    />
  </div>
</template>

<script>
import schedule from '../lib/schedule.js'
import TrainingWeek from './TrainingWeek.vue'

export default {
  name: 'TrainingSchedule',
  props: {
    raceDay: {
      type: Date,
      required: true,
    },
  },
  components: {
    TrainingWeek,
  },
  computed: {
    schedule() {
      return schedule
    },
  },
}
</script>
