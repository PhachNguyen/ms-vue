<template>
  <div class="main-content-table">
    <div class="table-wrapper">
      <div class="ms-table">
        <table>
          <!-- Header -->
          <thead>
            <!-- Dùng for truyền các fields vào header table -->
            <tr>
              <th class="btn-checkbox header display-flex align-items-center">
                <input class="btn-check" type="checkbox" />
              </th>
              <th v-for="field in fields" :key="field.key">{{ field.label }}</th>
              <!-- <slot :name="'Header-' + field.key"> {{ field.label }} </slot> -->
            </tr>
          </thead>
          <tbody>
            <!-- For dùng để chạy một hàng  -->
            <tr v-for="(row, rowIndex) in rows" :key="rowIndex" class="table-row">
              <!-- <h1>{{ rowIndex }}</h1> -->
              <!--  Tạo ra một slot để custom lại cái header checkbox -->
              <!--  Đặt name theo key -->
              <td class="btn-checkbox">
                <input class="btn-check" type="checkbox" />
              </td>
              <!-- Sau khi chạy mỗi hàng xong thì vừa chạy hàng for column -->
              <td v-for="field in fields" :key="field.key">
                <!-- Render khi vào column custom  -->
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
    <div
      class="main-content-bottom display-flex flex-row justify-content-space-between align-items-center"
    >
      <div class="total">
        Tổng: <span style="font-weight: 700">{{ total }}</span> bản ghi
      </div>
      <div
        class="bottom-right display-flex justify-content-space-between align-items-center flex-row"
      >
        <span class="title-pagination">Số bản ghi/trang</span>
        <div class="pagination display-flex flex-row align-items-center">
          <span style="padding-right: 8px">25</span>
          <div class="icon-pagination"></div>
        </div>
        <div class="number-pagination display-flex">
          <span style="padding-left: 6px">1 <span style="padding: 5px">-</span> 25 bàn ghi </span>
          <div class="icon-left"></div>
          <div class="icon-right"></div>
        </div>
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
  total: {
    type: Number,
    default: 0,
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
  switch (type) {
    case 'number':
      return formatNumber(value)
    case 'date':
      return formatDate(value)
    case 'text':
      return formatText(value)
    default:
      return formatText(value)
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
  /* height: 15%; */
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
  height: 430px; /* chiều cao trừ phần bottom */
  flex: 1;
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

.cell-name {
  display: flex;
  align-items: center;
  gap: 10px;
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
.main-content-bottom {
  font-size: 14px;
  /* height: 36px; */

  padding: 12px;
  background-color: #f5f5f5;
  color: #394856;
}
.main-content-bottom .total {
  font-weight: 700px;
}
.main-content-bottom .pagination {
  padding: 7px 16px;
  border: 0.8px;
  background-color: #ffffff;
}
.main-content-bottom .title-pagination {
  margin-right: 13px;
  /* margin-top: 9px; */
  font-size: 14px;
  font-weight: 400px;
  /* border: 1px solid gray; */
}
.main-content-bottom .number-pagination {
  /* margin-top: 2px; */
}
.main-content-bottom .icon-dropdown {
}
.main-content-bottom .icon-left {
  margin-left: 16px;
  padding-right: 7px;
}
</style>
