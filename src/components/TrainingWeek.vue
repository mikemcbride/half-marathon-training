<template lang="html">
  <div
    class="bg-white shadow rounded mb-4 px-6 pt-6 pb-2 md:pb-6"
    :class="{
      'bg-indigo-lightest text-indigo-dark border-2 border-indigo-light': isActiveWeek,
      'opacity-50': isInPast,
    }"
    @click="toggleExpand"
  >
    <div class="flex justify-between">
      <h3 class="mb-4 md:mb-6">Week of {{ formattedStartDate }}</h3>
      <span v-if="canExpand">
        <span v-show="!isExpanded">&#9660;</span>
        <span v-show="isExpanded">&#9650;</span>
      </span>
    </div>
    <transition name="fade">
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
    </transition>
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

<style lang="css">
.fade-enter-active,
.fade-leave-active {
  transition: opacity .3s ease
}

.fade-enter,
.fade-leave-to {
  opacity: 0
}

</style>
