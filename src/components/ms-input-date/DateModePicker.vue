<script setup>
import { ref, watch } from 'vue'
import { DownOutlined } from '@ant-design/icons-vue'

const props = defineProps({
  label: String,
  type: {
    type: String,
    default: 'date',
    validator: (v) => ['date', 'month', 'year'].includes(v),
  },
})

//
const modelValue = defineModel()

//State nội bộ
const dateValue = ref(modelValue.value)

// Mode + format
const currentMode = ref('date')
const currentFormat = ref('DD/MM/YYYY')
const currentLabel = ref('Ngày tháng năm')
const currentPlaceholder = ref('dd/MM/yyyy')

// Hàm đổi mode
function setMode(mode) {
  if (mode === 'year') {
    currentMode.value = 'year'
    currentFormat.value = 'YYYY'
    currentLabel.value = 'Năm'
    currentPlaceholder.value = 'yyyy'
  } else if (mode === 'month') {
    currentMode.value = 'month'
    currentFormat.value = 'MM/YYYY'
    currentLabel.value = 'Tháng năm'
    currentPlaceholder.value = 'MM/yyyy'
  } else {
    currentMode.value = 'date'
    currentFormat.value = 'DD/MM/YYYY'
    currentLabel.value = 'Ngày tháng năm'
    currentPlaceholder.value = 'dd/MM/yyyy'
  }
}

// Khi props.type thay đổi cập nhật mode
watch(
  () => props.type,
  (v) => setMode(v),
  { immediate: true },
)

//
watch(dateValue, (v) => {
  modelValue.value = v
})

//
watch(modelValue, (v) => {
  dateValue.value = v
})
</script>

<template>
  <div class="date-mode-wrapper display-flex flex-column">
    <div class="display-flex justify-content-space-between">
      <label v-if="props.label" class="date-label">{{ props.label }}</label>

      <div v-if="props.type === 'date'">
        <a-dropdown placement="bottomLeft">
          <a class="mode-btn" @click.prevent> {{ currentLabel }} <DownOutlined /> </a>
          <template #overlay>
            <a-menu>
              <a-menu-item @click="setMode('year')">Năm</a-menu-item>
              <a-menu-item @click="setMode('month')">Tháng năm</a-menu-item>
              <a-menu-item @click="setMode('date')">Ngày tháng năm</a-menu-item>
            </a-menu>
          </template>
        </a-dropdown>
      </div>
    </div>

    <a-date-picker
      v-model:value="dateValue"
      :format="currentFormat"
      :picker="currentMode"
      :placeholder="currentPlaceholder"
      style="width: 100%"
    />
  </div>
</template>

<style scoped>
.mode-btn {
  color: #b7b7b7;
}
.date-label {
  font-size: 14px;
  font-weight: 500;
  color: #374151;
}
</style>
