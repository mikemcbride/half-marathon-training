<template lang="html">
  <div>
    <TrainingWeek
      v-for="(workouts, $index) in schedule"
      :key="$index"
      :week="$index"
      :workouts="workouts"
      :race-day="raceDay" />
  </div>
</template>

<script>
import schedule from '@/assets/schedule'
import TrainingWeek from '@/components/TrainingWeek'

export default {
  name: 'TrainingSchedule',
  props: {
    raceDay: {
      type: Date,
      required: true
    },
  },
  components: {
    TrainingWeek,
  },
  computed: {
    schedule() {
      return schedule
    }
  },
}
</script>
