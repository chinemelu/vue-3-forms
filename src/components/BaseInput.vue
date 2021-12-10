<template>
  <label :for="uuid">{{ label }}</label>
  <input
    :id="uuid"
    :aria-invalid="error ? true : null"
    v-bind="{
      ...$attrs,
      onInput: handleInput
    }"
    :value="modelValue"
    :aria-describedby="error ? `${uuid}-error` : null"
  />
  <p aria-live="assertive" :id="`${uuid}-error`" v-if="error" class="errorMessage">{{error}}</p>
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
      required: true
    },
    error: {
      type: String,
      default: ''
    }
  },
  setup (props, { emit }) {
    const handleInput = (event) => {
      emit('update:modelValue', event.target.value)
    }

    const uuid = UniqueID().getID()

    return { handleInput, uuid }
  }
}
</script>

<style>

</style>
