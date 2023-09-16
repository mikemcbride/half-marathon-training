<template lang="html">
  <label class="flex items-start md:items-center justify-start flex-col md:flex-row gap-2">
    <div class="block text-sm font-medium leading-6 text-gray-900">{{ label }}</div>
    <div class="relative rounded-md shadow-sm">
      <input type="date" v-bind="$attrs" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"
        class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-blue-600 sm:text-sm sm:leading-6" />
    </div>
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
