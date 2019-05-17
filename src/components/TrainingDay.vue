<template lang="html">
  <div class="mb-4 md:mb-0" :class="{'text-yellow': activeDay}">
    <div class="uppercase mb-2 text-xs font-normal opacity-75">
      {{ date }}
    </div>
    <div class="font-semibold text-xl">{{ workout }}</div>
  </div>
</template>

<script>
import format from 'date-fns/format'
import isToday from 'date-fns/is_today'

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
      return format(this.day, 'dddd')
    },
    activeDay() {
      return isToday(this.day)
    }
  },
}
</script>
