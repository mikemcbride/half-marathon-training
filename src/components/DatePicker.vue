<template lang="html">
  <label class="block md:flex items-center">
    <div v-if="label !== ''" class="font-semibold mb-2 md:mb-0 mr-4">
      {{ label }}
    </div>
    <input
      type="date"
      v-bind="$attrs"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      class="w-full md:w-auto rounded p-2 font-base border border-grey hover:border-grey-darker focus:outline-none focus:border-indigo"
    />
  </label>
</template>

<script>
export default {
  name: 'DatePicker',
  props: {
    modelValue: {
      type: [String, Number, Date],
      required: true,
    },
    label: {
      type: String,
      default: '',
    },
  },
  emits: ['update:modelValue']
}
</script>
