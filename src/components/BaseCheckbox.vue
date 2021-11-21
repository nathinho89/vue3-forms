<template>
    <div>
        <input
          :id="uuid"
          :checked="modelValue"
          @change="$emit('update:modelValue', $event.target.checked)"
          type="checkbox"
          class="field"
        />
        <label v-if="label" :for="uuid">{{ label }}</label>
      </div>
</template>

<script>
import UniqueID from '../features/UniqueID'

export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: Boolean,
      default: false
    }
  },
  setup () {
    const uuid = UniqueID().getID()
    return {
      uuid
    }
  }
}
</script>
