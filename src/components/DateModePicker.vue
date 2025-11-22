<script setup>
import { ref, watch } from 'vue'
import { DownOutlined } from '@ant-design/icons-vue'

// 🟦 Props tái sử dụng
const props = defineProps({
  label: String,
  type: {
    type: String,
    default: 'date', // date | month | year
    validator: (v) => ['date', 'month', 'year'].includes(v),
  },
})

// 🟦 Giá trị ngày trả ra ngoài
const dateValue = ref(null)

// 🟦 Mode + Format + Label (mutable)
const currentMode = ref('date')
const currentFormat = ref('DD/MM/YYYY')
const currentLabel = ref('Ngày tháng năm')
const currentPlaceholder = ref('dd/MM/yyyy')

// 🟦 Đổi mode khi props thay đổi hoặc khi người dùng nhấn menu
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

// 🟦 Áp dụng props ban đầu
// watch(
//   () => props.type,
//   (value) => setMode(value),
//   { immediate: true },
// )

// 🟦 Khi click chọn mode
function changeMode(mode) {
  setMode(mode)
}
</script>
<template>
  <div class="date-mode-wrapper display-flex flex-column">
    <!-- DatePicker -->
    <div class="display-flex justify-content-space-between">
      <div v-if="props.label" class="date-label">{{ props.label }}</div>
      <div v-if="props.type === 'date'">
        <a-dropdown placement="bottomLeft">
          <a class="mode-btn" @click.prevent> {{ currentLabel }} <DownOutlined /> </a>
          <template #overlay>
            <a-menu>
              <a-menu-item @click="changeMode('year')">Năm</a-menu-item>
              <a-menu-item @click="changeMode('month')">Tháng năm</a-menu-item>
              <a-menu-item @click="changeMode('date')">Ngày tháng năm</a-menu-item>
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

    <!-- Dropdown -->
  </div>
</template>
<style scoped>
.mode-btn {
  color: #b7b7b7;
}
.date-label {
  color: #374151;
}
</style>
>
