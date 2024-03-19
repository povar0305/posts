<script lang="ts" setup>
const props = defineProps<{
  modelValue: string
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', text: string): void
}>()
</script>

<template>
  <div class="wrapper">
    <input :value="modelValue" type="text" @input="$emit('update:modelValue',$event.target.value)"/>
  </div>
</template>

<style lang="scss" scoped>
@import './assets/style/main.scss';

.wrapper {
  position: relative;
  margin-bottom: 16px;
}

input {
  padding: 8px 16px;
  outline: none;
  border: 1px solid $gray-color;
  border-radius: 4px;
}
</style>