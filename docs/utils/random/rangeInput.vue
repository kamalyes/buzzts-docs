<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'RangeInput',
  props: {
    label: String,
    min: Number,
    max: Number,
    modelValue: {
      type: Array,
      required: true,
      validator: (val: unknown) => {
        return (
          Array.isArray(val) &&
          val.length === 2 &&
          typeof val[0] === 'number' &&
          typeof val[1] === 'number'
        );
      }
    }
  },
  emits: ['update:modelValue'],
  methods: {
    updateStart(value: number) {
      if (value > this.modelValue[1]) value = this.modelValue[1];
      this.$emit('update:modelValue', [value, this.modelValue[1]]);
    },
    updateEnd(value: number) {
      if (value < this.modelValue[0]) value = this.modelValue[0];
      this.$emit('update:modelValue', [this.modelValue[0], value]);
    }
  }
});
</script>

<template>
  <div style="display: flex; align-items: center; gap: 18px;">
    <label style="min-width: 80px;">{{ label }}</label>
    <n-input-number
      :min="min"
      :max="modelValue[1]"
      :value="modelValue[0]"
      @update:value="updateStart"
      style="width: 100px"
    />
    <span>-</span>
    <n-input-number
      :min="modelValue[0]"
      :max="max"
      :value="modelValue[1]"
      @update:value="updateEnd"
      style="width: 100px"
    />
  </div>
</template>
