<script setup>
import UniqueID from "@/features/UniqueID";
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
    type: [String, Number]
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
    :checked="modelValue === value"
    v-bind="{
      ...$attrs,
      onChange: $event => {
        $emit('update:modelValue', $event.target.value);
      }
    }"
  />
  <label :for="uuid" v-if="label">{{ label }}</label>

  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>
