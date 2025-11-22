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
      <template #Name="{ row, value }">
        <div style="display: flex; flex-direction: row">
          <strong>{{ value }}</strong>
          <div v-if="row.IsUser" style="color: green">
            <div class="icon-setting"></div>
            Nhân viên
          </div>
        </div>
      </template>
    </MsTable>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MsTable from '@/components/ms-table/MsTable.vue'
import candidate from '../data/candidate-data.json'
// import MsButton from '@/components/ms-button/MsButton.vue'

//#region Static Data
//  Header của table
const fields = [
  // { key: 'Select', label: '', type: 'custom' }, // checkbox
  { key: 'Name', label: 'Họ và tên', type: 'custom' },

  { key: 'Phone', label: 'Số điện thoại', type: 'text' },
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
const rows = ref(JSON.parse(localStorage.getItem('candidateList') || '[]'))
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
</style>
