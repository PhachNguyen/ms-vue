<script setup>
const model = defineModel()

const props = defineProps({
  label: String,
  placeholder: String,
  type: { type: String, default: 'text' }, // text | select
  required: Boolean,
  options: { type: Array, default: () => [] }, // select options
})
</script>

<template>
  <div class="ms-input-wrapper display-flex flex-column">
    <!-- LABEL -->
    <label class="label-input">
      {{ props.label }}
      <span v-if="props.required" class="required">*</span>
    </label>

    <!-- INPUT -->
    <input
      v-if="props.type !== 'select'"
      :type="props.type"
      class="dx-input"
      :placeholder="props.placeholder"
      v-model="model"
    />

    <!-- SELECT -->
    <a-select
      v-else
      v-model:value="model"
      :placeholder="props.placeholder"
      show-search
      :options="props.options"
      :filter-option="(input, option) => option.label.toLowerCase().includes(input.toLowerCase())"
      class="ms-select"
    />
  </div>
</template>

<style scoped>
.ms-input-wrapper {
  width: 100%;
}

.label-input {
  font-size: 14px;
  font-weight: 500;
  color: #374151;
  /* margin-bottom: 6px; */
}

.required {
  color: #e91e63;
}

/* INPUT STYLE */
.dx-input {
  /* width: 100%; */
  height: 22px;
  padding: 8px 12px;
  border: 1px solid #d0d5dd;
  border-radius: 6px;
  font-size: 14px;
  outline: none;
  transition: all 0.15s ease;
}

.dx-input:hover {
  border-color: #a6b0b9;
}

.dx-input:focus {
  border-color: #4a90e2;
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.25);
}

/*  */
.ms-select :deep(.ant-select-selector) {
  /* height: 36px !important; */
  display: flex;
  align-items: center;
  border-radius: 6px !important;
}

.ms-select :deep(.ant-select-selection-placeholder) {
  color: #9ca3af;
}
</style>
