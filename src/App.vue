<template>
  <div id="app" class="font-sans text-grey-darkest mx-auto p-4 block max-w-xl">
    <header class="md:flex justify-between mb-6">
      <h1 class="mb-8 md:mb-0">Half Marathon Training</h1>
      <DatePicker
        v-model="raceDay"
        @change="updateRaceDay"
        label="Race date"
        class="mb-6 md:mb-0"
      />
    </header>
    <TrainingSchedule v-if="raceDate" :race-day="raceDate" />
  </div>
</template>

<script>
import DatePicker from '@/components/DatePicker'
import TrainingSchedule from '@/components/TrainingSchedule'
import parse from 'date-fns/parse'

export default {
  name: 'app',
  components: {
    DatePicker,
    TrainingSchedule,
  },
  data() {
    return {
      raceDay: '',
    }
  },
  computed: {
    raceDate() {
      if (this.raceDay === '') {
        return
      }

      return parse(this.raceDay)
    },
  },
  methods: {
    updateRaceDay() {
      if (this.raceDay === '') {
        window.localStorage.removeItem('mcbrideHalfMarathonTraining')
      } else {
        window.localStorage.setItem('mcbrideHalfMarathonTraining', this.raceDay)
      }
    },
  },
  created() {
    // remember your race date if you've set it before
    let raceDay = window.localStorage.getItem('mcbrideHalfMarathonTraining')
    if (raceDay !== null) {
      this.raceDay = raceDay
    }
  },
}
</script>

<style>
@tailwind preflight;
@tailwind components;
@tailwind utilities;
</style>
