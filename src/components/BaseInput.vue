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
  error: {
    type: String,
    default: ""
  }
});

const uuid = UniqueID().getID();
</script>

<template>
  <label :for="uuid" v-if="label">{{ label }}</label>
  <input
    :value="modelValue"
    :placeholder="label"
    :id="uuid"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : null"
    class="field"
    v-bind="{
      ...$attrs,
      onInput: $event => {
        $emit('update:modelValue', $event.target.value);
      }
    }"
  />

  <p
    v-if="error"
    class="errorMessage"
    :id="`${uuid}-error`"
    aria-live="assertive"
  >
    {{ error }}
  </p>
</template>
