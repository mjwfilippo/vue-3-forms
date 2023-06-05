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
    class="field"
    :id="uuid"
    :value="modelValue"
    :placeholder="label"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : null"
    :class="{ error }"
    v-bind="{
      ...$attrs,
      onInput: $event => {
        $emit('update:modelValue', $event.target.value);
      }
    }"
  />

  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>
