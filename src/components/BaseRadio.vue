<script setup>
import UniqueID from "../features/UniqueID";
import BaseErrorMessage from "./BaseErrorMessage.vue";

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
  },
  error: {
    type: String,
    default: ""
  }
});
const uuid = UniqueID().getID();
</script>

<template>
  <input
    type="radio"
    :id="uuid"
    :value="value"
    :checked="modelValue === value"
    v-bind="$attrs"
    @change="$emit('update:modelValue', value)"
  />
  <label :for="uuid" v-if="label">{{ label }}</label>

  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>
