<template>
  <div class="main-content-table">
    <div class="table-wrapper">
      <div class="ms-table">
        <table>
          <thead>
            <!-- Dùng for truyền các fields vào header table -->
            <tr>
              <div class="btn-checkbox header display-flex align-items-center">
                <input class="btn-check" type="checkbox" />
              </div>
              <th v-for="field in fields" :key="field.key">{{ field.label }}</th>
              <!-- <slot :name="'Header-' + field.key"> {{ field.label }} </slot> -->
            </tr>
          </thead>
          <tbody>
            <!-- For dùng để chạy một hàng  -->
            <tr v-for="(row, rowIndex) in rows" :key="rowIndex" class="table-row">
              <!--  Tạo ra một slot để custom lại cái header checkbox -->
              <!--  Đặt name theo key -->
              <div class="btn-checkbox display-flex align-items-center">
                <input class="btn-check" type="checkbox" />
              </div>
              <!-- Sau khi chạy mỗi hàng xong thì vừa chạy hàng for column -->
              <td v-for="field in fields" :key="field.key">
                <!-- Custom type with slot -->
                <template v-if="field.type === 'custom'">
                  <!--  Định nghĩa biến slot -->
                  <slot :name="field.key" :row="row" :field="field" :value="row[field.key]">
                    {{ handleFormat(row[field.key], 'text') }}
                  </slot>
                </template>

                <!-- Other types -->
                <template v-else>
                  {{ handleFormat(row[field.key], field.type || 'text') }}
                </template>
              </td>
              <!-- Floating action buttons -->
              <!-- <div class="action-buttons">
            <button @click="handleEdit(row)" class="edit-btn">Edit</button>
            <button @click="handleDelete(row)" class="delete-btn">Delete</button>
          </div> -->
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { formatNumber, formatDate, formatText } from '@/utils/formatter'

//#region Props

const props = defineProps({
  //  Thông tin header
  fields: {
    type: Array,
    required: true,
    // Validate
    validator: (value) => {
      return value.every((field) => {
        const validTypes = ['text', 'number', 'date', 'custom', 'checkbox']
        return field.key && field.label && validTypes.includes(field.type || 'text')
      })
    },
  },
  // Các row
  rows: {
    type: Array,
    required: true,
  },
})
//#endregion

//#region Emits
const emit = defineEmits(['edit', 'delete'])
//#endregion

//#region Methods
/**
 * Hàm định dạng giá trị dựa trên kiểu
 * @param value
 * @param type
 * @returns
 * createdby: pdthien - 15.10.2025
 */
const handleFormat = (value, type) => {
  if (value === null || value === undefined) return ''

  // Nếu array → join cho đẹp
  if (Array.isArray(value)) return value.join(', ')

  switch (type) {
    case 'number':
      return Number(value).toLocaleString('vi-VN')
    case 'date':
      return new Date(value).toLocaleDateString('vi-VN')
    default:
      return String(value)
  }
}
// Handle click lưu hết all
/**
 * Hàm xử lý sửa bản ghi
 * @param row

 */
const handleEdit = (row) => {
  emit('edit', row)
}

/**
 * Hàm xử lý xóa bản ghi
 * @param row
 * với const row
 * createdby: pdthien - 15.10.2025
 */
const handleDelete = (row) => {
  emit('delete', row)
}
//#endregion
</script>

<style scoped>
/* TABLE  */
/* Vùng table trong trang */
.main-content-table {
  height: 95%;
  margin-top: 16px;
  padding: 0 24px;
}
.btn-checkbox {
  padding: 10px;
}
.btn-checkbox.header {
  background: #f9fafb;
}
/* Bọc table để scroll ngang */
.table-wrapper {
  overflow: auto;
  width: 100%;
  height: 100%;
  border-radius: 6px;
}

/* Table */
.ms-table {
  width: max-content;
  border-collapse: collapse;
  background: white;
  font-size: 14px;
  height: 100%;
}

/* Header */
.ms-table thead th {
  text-align: left;
  font-weight: 600;
  padding: 12px 20px;
  border-bottom: 1px solid #e5e7eb;
  background: #f9fafb;
  white-space: nowrap; /* tránh xuống dòng */
}

/* Body */
.ms-table tbody td {
  padding: 14px 20px;
  border-bottom: 1px solid #eaecef;
  white-space: nowrap;
}

/* Checkbox */
.ms-table input[type='checkbox'] {
  width: 16px;
  height: 16px;
}

/* Tên + Avatar */
.cell-name {
  display: flex;
  align-items: center;
  gap: 10px;
}

.avatar {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  color: white;
  font-weight: 600;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
}
.table-row {
  position: relative;
}

.table-row:hover {
  background-color: #f5f5f5;
  color: black;
}

.table-row:hover .action-buttons {
  opacity: 1;
  pointer-events: auto;
}

.action-buttons {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  gap: 0.5rem;
  padding: 0 1rem;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.2s ease;
  background: linear-gradient(to left, #f5f5f5 70%, transparent);
}

.edit-btn,
.delete-btn {
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  cursor: pointer;
  z-index: 1;
}

.edit-btn {
  background-color: #4caf50;
  color: white;
  border: none;
}

.delete-btn {
  background-color: #f44336;
  color: white;
  border: none;
}

.edit-btn:hover,
.delete-btn:hover {
  opacity: 0.9;
}
.btn-check {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
