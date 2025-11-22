<script></script>
<template>
  <div class="main-content-table">
    <div class="table-wrapper">
      <table class="candidate-table">
        <thead>
          <tr>
            <th><input type="checkbox" /></th>
            <th>Họ và tên</th>
            <th>Số điện thoại</th>
            <th>Email</th>
            <th>Chiến dịch tuyển dụng</th>
            <th>Vị trí tuyển dụng</th>
            <th>Vòng tuyển dụng</th>
            <th>Đánh giá</th>
            <th>Ngày ứng tuyển</th>
            <th>Người giới thiệu</th>
            <th>Thông tin tiếp nhận</th>
            <th>Thông tin tiếp nhận</th>
            <th>Thuộc kho tiềm năng</th>
            <th>Tài khoản cổng ứng viên</th>
            <th>Thẻ</th>
            <th>Trạng thái</th>
            <th>Giới tính</th>
            <th>Ngày sinh</th>
            <th>Địa chỉ</th>
            <th>Lý do loại</th>
            <th>Cộng tác viên</th>
            <th>Ngày tiếp nhận</th>
            <th>Trạng thái</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
/* TABLE  */
/* Vùng table trong trang */
.main-content-table {
  height: 70%;
  margin-top: 16px;
  padding: 0 24px;
}

/* Bọc table để scroll ngang */
.table-wrapper {
  overflow: auto;
  width: 100%;
  height: 100%;
  border-radius: 6px;
}

/* Table */
.candidate-table {
  width: max-content;
  border-collapse: collapse;
  background: white;
  font-size: 14px;
  height: 100%;
}

/* Header */
.candidate-table thead th {
  text-align: left;
  font-weight: 600;
  padding: 12px 20px;
  border-bottom: 1px solid #e5e7eb;
  background: #f9fafb;
  white-space: nowrap; /* tránh xuống dòng */
}

/* Body */
.candidate-table tbody td {
  padding: 14px 20px;
  border-bottom: 1px solid #eaecef;
  white-space: nowrap;
}

/* Checkbox */
.candidate-table input[type='checkbox'] {
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
</style>
