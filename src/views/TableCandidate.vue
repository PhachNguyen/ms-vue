<template>
  <div>
    <!-- <div class="card">
      <ms-button type="primary" icon="fa-car" @click="count++">Number is: {{ count }}</ms-button>
    </div> -->

    <!--  Dùng component table vô -->
    <!-- Tạm thời chưa cần @edit="handleEdit" @delete="handleDelete" -->
    <MsTable :fields="fields" :rows="rows">
      <!-- Header select -->

      <!--  Name -->
      <template #Name="{ value }">
        <span style="display: inline-flex; align-items: center; justify-content: center; gap: 8px">
          <div class="avatar-warp">
            <Avatar
              :name="value"
              bgColor="#1876c7"
              color="#fff"
              size="23"
              style="display: inline-flex; align-items: center; gap: 8px"
            />
          </div>
          <strong>{{ value }}</strong>
        </span>
      </template>
    </MsTable>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Avatar from 'vue3-avatar'

import MsTable from '@/components/ms-table/MsTable.vue'
import candidate from '../data/candidate-data.json'
// import MsButton from '@/components/ms-button/MsButton.vue'

//#region Static Data
//  Header của table
const fields = [
  // { key: 'Select', label: '', type: 'custom' }, // checkbox
  { key: 'Name', label: 'Họ và tên', type: 'custom' },

  { key: 'Phone', label: 'Số điện thoại', type: 'number' },
  { key: 'Email', label: 'Email', type: 'text' },

  { key: 'Campaign', label: 'Chiến dịch tuyển dụng', type: 'text' },
  { key: 'Position', label: 'Vị trí tuyển dụng', type: 'text' },
  { key: 'Round', label: 'Vòng tuyển dụng', type: 'text' },
  { key: 'Rating', label: 'Đánh giá', type: 'text' },

  { key: 'AppliedDate', label: 'Ngày ứng tuyển', type: 'date' },
  { key: 'Referrer', label: 'Người giới thiệu', type: 'text' },

  { key: 'ReceivedInfo1', label: 'Thông tin tiếp nhận', type: 'text' },
  { key: 'ReceivedInfo2', label: 'Thông tin tiếp nhận', type: 'text' },

  { key: 'Potential', label: 'Thuộc kho tiềm năng', type: 'text' },
  { key: 'PortalAccount', label: 'Tài khoản cổng ứng viên', type: 'text' },
  { key: 'Tags', label: 'Thẻ', type: 'text' },

  { key: 'Status', label: 'Trạng thái', type: 'text' },

  { key: 'Gender', label: 'Giới tính', type: 'text' },
  { key: 'BirthDate', label: 'Ngày sinh', type: 'date' },
  { key: 'Address', label: 'Địa chỉ', type: 'text' },

  { key: 'RejectReason', label: 'Lý do loại', type: 'text' },
  { key: 'Collaborator', label: 'Cộng tác viên', type: 'text' },

  { key: 'ReceivedDate', label: 'Ngày tiếp nhận', type: 'date' },
  { key: 'ReceiveStatus', label: 'Trạng thái tiếp nhận', type: 'text' },
]

//#endregion

//#region State Data

const count = ref(0)
//  Giá trị hàng
// const rows = ref(JSON.parse(localStorage.getItem('candidateList') || '[]'))
const props = defineProps({
  rows: {
    type: Array,
  },
})
console.log(props.rows.value)
// console.log('Giá trj row' + rows.value)
//#endregion

//#endregion

//#region Methods
/**
 * Hàm xử lý sửa bản ghi
 * @param row

 */
const handleEdit = (row) => {
  console.log('Edit:', row)
}

/**
 * Hàm xử lý xóa bản ghi
 * @param row
 * createdby: pdthien - 15.10.2025
 */
const handleDelete = (row) => {
  rows.value = rows.value.filter((item) => item.Id !== row.Id)
}
//#endregion
</script>

<style scoped>
/* TABLE  */
/* Tắt img avt */
:deep(.container) {
  display: inline-block !important;
  padding: 0 !important;
  margin: 0 !important;
  height: auto !important;
  width: auto !important;
  background: transparent !important;
}
</style>
