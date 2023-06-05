<script setup>
import UniqueID from "@/features/UniqueID";
import BaseErrorMessage from "./BaseErrorMessage.vue";

defineProps({
  label: {
    type: String,
    default: ""
  },
  modelValue: {
    type: Boolean
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
    type="checkbox"
    class="field"
    :id="uuid"
    :checked="modelValue"
    v-bind="{
      ...$attrs,
      onChange: $event => {
        $emit('update:modelValue', $event.target.checked);
      }
    }"
  />
  <label :for="uuid" v-if="label">{{ label }}</label>
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>
