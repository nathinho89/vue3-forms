<template>
    <component
        v-for="option in options"
        :key="option.value"
        :is="vertical ? 'div' : 'span'">
        <BaseRadio
            :label="option.label"
            :value="option.value"
            :name="name"
            :modelValue="modelValue"
            @update:modelValue="$emit('update:modelValue', $event)"/>
    </component>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: [String, Number, Boolean],
      required: true
    },
    name: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      required: true
    },
    vertical: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="css" scoped>
  span {
    margin-right:1rem;
  }
</style>
