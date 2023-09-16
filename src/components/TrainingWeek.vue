<template>
  <div
    class="bg-white shadow rounded mb-4 px-4 pt-6 pb-2 md:pb-6"
    :class="{
      'bg-indigo-50 text-indigo-700 border border-indigo-100': isActiveWeek,
      'opacity-50': isInPast,
    }"
    @click="toggleExpand"
  >
    <div class="flex justify-between">
      <h3 class="px-2 mb-4">Week of {{ formattedStartDate }}</h3>
      <span v-if="canExpand">
        <span v-show="!isExpanded">&#9660;</span>
        <span v-show="isExpanded">&#9650;</span>
      </span>
    </div>
    <div
      v-if="isExpanded"
      class="flex flex-col md:flex-row justify-between">
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
import { subWeeks, addDays, format, isSameWeek, isPast } from 'date-fns'
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
    isActiveWeek() {
      const weekStartsOn = this.startDate.getDay()
      const today = new Date()
      return isSameWeek(today, this.startDate, { weekStartsOn })
    },
    isInPast() {
      if (this.isActiveWeek === true) {
        return false
      }

      return isPast(this.startDate)
    },
  },
  data() {
    return {
      canExpand: true,
      isExpanded: false
    }
  },
  mounted() {
    // reverse if not on mobile
    if (window.innerWidth >= 768) {
      this.isExpanded = true
      this.canExpand = false
    }
  },
  methods: {
    toggleExpand() {
      if (this.canExpand === true) {
        this.isExpanded = !this.isExpanded
      }
    }
  },
}
</script>
