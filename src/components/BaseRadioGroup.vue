<script setup>
import BaseRadio from "@/components/BaseRadio.vue";
defineProps({
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
});
</script>

<template>
  <component
    v-for="option in options"
    :key="option.value"
    :is="vertical ? 'div' : 'span'"
    :style="vertical ? '' : 'margin-right: 20px;'"
  >
    <BaseRadio
      :name="name"
      :label="option.label"
      :modelValue="modelValue"
      :value="option.value"
      @update:modelValue="$emit('update:modelValue', $event)"
    />
  </component>
</template>

<style scoped>
.horizontal {
  margin-right: 20px;
}
</style>
