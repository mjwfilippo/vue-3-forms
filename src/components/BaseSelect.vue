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
  options: {
    type: Array,
    required: true
  }
});
const uuid = UniqueID().getID();
</script>

<template>
  <label :for="uuid" v-if="label">{{ label }}</label>
  <select
    :value="modelValue"
    :id="uuid"
    class="field"
    v-bind="{
      ...$attrs,
      onChange: $event => {
        $emit('update:modelValue', $event.target.value);
      }
    }"
  >
    <option
      v-for="option in options"
      :value="option"
      :key="option"
      :selected="option === modelValue"
    >
      {{ option }}
    </option>
  </select>
</template>
