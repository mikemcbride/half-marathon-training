<template lang="html">
  <div class="mb-4 md:mb-0">
    <div class="uppercase mb-2 text-xs font-normal text-grey-darker">
      {{ date }}
    </div>
    <div class="font-semibold">{{ workout }}</div>
  </div>
</template>

<script>
import format from 'date-fns/format'

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
  },
}
</script>
