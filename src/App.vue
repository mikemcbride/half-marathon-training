<template>
  <div id="app" class="font-sans mx-auto p-4 block max-w-xl">
    <h1 class="mb-8">Half Marathon Training</h1>
    <DatePicker v-model="raceDay" label="Race date" />
    <TrainingSchedule v-if="raceDate" :race-day="raceDate" />
  </div>
</template>

<script>
import DatePicker from '@/components/DatePicker'
import TrainingSchedule from '@/components/TrainingSchedule'
import { parse } from 'date-fns'

export default {
  name: 'app',
  components: {
    DatePicker,
    TrainingSchedule
  },
  data() {
    return {
      raceDay: ''
    }
  },
  computed: {
    raceDate() {
      if (this.raceDay === '') {
        return
      }
      
      return parse(this.raceDay)
    }
  },
}
</script>

<style>
@tailwind preflight;
@tailwind components;
@tailwind utilities;
</style>
