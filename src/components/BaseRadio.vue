<script setup>
import UniqueID from "../features/UniqueID";

defineProps({
  label: {
    type: String,
    default: ""
  },
  modelValue: {
    type: [String, Number],
    default: ""
  },
  value: {
    type: [String, Number],
    required: true
  }
});
const uuid = UniqueID().getID();
</script>

<template>
  <input
    type="radio"
    :checked="modelValue === value"
    :value="value"
    :id="uuid"
    v-bind="{
      ...$attrs,
      onChange: $event => {
        $emit('update:modelValue', value);
      }
    }"
  />
  <label :for="uuid" v-if="label">{{ label }}</label>
</template>
