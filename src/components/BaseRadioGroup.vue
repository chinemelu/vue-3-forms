<template>
  <component
    :is="vertical ? 'div' : 'span'"
    v-for="(option, index) in options"
    :key="index"
    :class="{ horizontal: !vertical}"
  >
    <BaseRadio
      :value="option.value"
      :label="option.label"
      :name="name"
      :modelValue="modelValue"
      @update:modelValue="$emit('update:modelValue', option.value)"
    />
  </component>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    modelValue: {
      type: [String, Number],
      required: true
    },
    vertical: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
.horizontal {
  margin-right: 20px;
}
</style>
