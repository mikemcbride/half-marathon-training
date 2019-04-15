<template lang="html">
  <label class="block">
    <div v-if="label !== ''" class="font-semibold mb-2">
      {{ label }}
    </div>
    <input
      type="date"
      v-bind="$attrs"
      :value="value"
      v-on="listeners"
      class="w-full md:w-auto rounded-sm p-2 font-base border border-grey hover:border-grey-darker focus:outline-none focus:border-blue">
  </label>
</template>

<script>
export default {
  name: 'DatePicker',
  inheritAttrs: false,
  props: {
    value: {
      type: [String, Number],
      default: ''
    },
    label: {
      type: String,
      default: ''
    }
  },
  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: event => this.$emit('input', event.target.value)
      }
    }
  }
}
</script>
