<script setup>
defineProps({
  label: {
    type: String,
    default: ""
  },
  modelValue: {
    type: [String, Number],
    default: ""
  }
});
defineEmits(["update:modelValue"]);
</script>

<template>
  <label>{{ label }}</label>
  <input
    :value="modelValue"
    :placeholder="label"
    class="field"
    v-bind="{
      ...$attrs,
      onInput: $event => {
        $emit('update:modelValue', $event.target.value);
      }
    }"
  />
</template>
