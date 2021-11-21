<template>
    <input
        type="radio"
        :checked="modelValue === value"
        :value="value"
        @change="$emit('update:modelValue', value)"
        v-bind="$attrs"
        />
    <label v-if="label">{{ label }}</label>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      defualt: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    },
    value: {
      type: [String, Number],
      required: true
    }
  }
}
</script>
