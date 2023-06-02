<script setup>
import UniqueID from "../features/UniqueID";

defineProps({
  label: {
    type: String,
    default: ""
  },
  modelValue: {
    type: Boolean,
    default: false
  }
});

const uuid = UniqueID().getID();
</script>

<template>
  <input
    type="checkbox"
    :checked="modelValue"
    :id="uuid"
    class="field"
    @change="$emit('update:modelValue', $event.target.checked)"
  />
  <label :for="uuid" v-if="label">{{ label }}</label>
</template>
