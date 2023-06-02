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
  options: {
    type: Array,
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
  <label :for="uuid" v-if="label">{{ label }}</label>
  <select
    class="field"
    :id="uuid"
    :value="modelValue"
    v-bind="{
      ...$attrs,
      onChange: $event => {
        $emit('update:modelValue', $event.target.value);
      }
    }"
    aria-describedby="error ? `${uuid}-error` : null"
    aria-invalid="error ? true : false"
    :class="{ error }"
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
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>
