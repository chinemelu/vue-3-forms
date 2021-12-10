<template>
  <input
    type="radio"
    :checked="modelValue === value"
    :value="value"
    :id="uuid"
    v-bind="{
      ...$attrs,
      onChange: handleRadioButtonChange
    }"

  />
  <label :for="uuid">{{label}}</label>
</template>

<script>
import UniqueID from '../features/UniqueID.js'
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    },
    value: {
      type: [String, Number],
      required: true
    }
  },
  setup (props, { emit }) {
    const handleRadioButtonChange = (event) => {
      emit('update:modelValue', event.target.value)
    }
    const uuid = UniqueID().getID()
    return { handleRadioButtonChange, uuid }
  }
}
</script>

<style lang="scss" scoped>

</style>
