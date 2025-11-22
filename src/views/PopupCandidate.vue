// Luồng sự kiện từ component button emit lên maincontent -> app.vue
<script setup>
import { reactive, ref, watch } from 'vue'
import MsInput from '@/components/ms-input/MsInput.vue'
import DateModePicker from '@/components/DateModePicker.vue'

//  Init một Props
const Props = defineProps({
  isOpen: Boolean,
})

const emit = defineEmits(['update:isOpen'])
//  Tạo model
const model = defineModel()

function closeClick() {
  // debugger
  model.value = false
}
const form = reactive({
  fullName: '',
  dob: null,
  gender: null,
  phone: '',
  region: null,
  email: '',
  address: '',
  eduLevel: '',
  eduPlace: '',
  major: '',
  applyDate: '',
  source: '',
  recruiter: '',
  partner: '',
  lastCompany: '',
  position: '',
  startTime: '',
  endTime: '',
})
// Gender
const gender = [
  { label: 'Nam', value: 'male' },
  { label: 'Nữ', value: 'female' },
]

// const rules = {
//   fullName: [{ required: true, message: 'Không được để trống' }],
//   gender: [{ required: true, message: 'Vui lòng chọn giới tính' }],
//   phone: [{ required: true, message: 'Không được để trống' }],
// }
</script>
<template>
  <div class="model">
    <div>
      <!-- Overlay -->
      <div class="overlay" id="overlay " :class="{ show: model }"></div>
      <!-- Popup thêm -->
      <!-- Container -->
      <div class="modal modal-add display-flex flex-column" :class="{ show: model }">
        <!-- Title header pop-up -->
        <div
          class="modal-header display-flex justify-content-space-between align-items-center flex-row"
        >
          <div class="title-header">Thêm ứng viên</div>
          <div class="icon-close" id="closeModal" @click="closeClick"></div>
        </div>
        <!-- Content -->

        <div class="modal-content display-flex flex-column">
          <!-- Upload popup -->
          <div
            class="upload-box display-flex justify-content-center align-items-center flex-column"
          >
            <input
              type="file"
              id="cvUpload"
              name="cv"
              multiple
              accept=".doc,.docx,.pdf,.jpg,.jpeg,.png"
              hidden
            />
            <label for="cvUpload" class="upload-label">
              <span class="title display-flex justify-content-center"
                >Kéo và thả tệp vào đây để tải CV lên</span
              >
              <p class="sub-title">
                Chấp nhận file .doc, .docx, .pdf, .jpeg, .png (Dung lượng < 15 Mb).
              </p>
            </label>
          </div>
          <!--  Main- content popup -->
          <!-- Infor  -->
          <div class="modal-content-add display-flex flex1 flex-row">
            <!-- Content left -->
            <div class="modal-content-left">
              <div class="avatar-box display-flex justify-content-center align-items-center">
                <h2 class="image-add" style="font-size: 13px; color: rgb(178, 178, 178)">Ảnh</h2>
              </div>
            </div>
            <!-- Content-right -->
            <a-form :model="form" :rules="rules">
              <div class="modal-content-right flex1">
                <div class="form-container display-flex flex-column">
                  <!-- Họ tên -->
                  <!-- Họ và tên -->
                  <ms-input
                    label="Họ và tên"
                    name="fullName"
                    v-model="form.fullName"
                    placeholder="Nhập họ và tên"
                    required
                  />

                  <!-- Row Ngày sinh & Giới tính -->
                  <div
                    class="form-row display-flex flex-row justify-content-center align-items-center"
                  >
                    <!-- Nhóm label và icon -->
                    <!-- <label for="">Ngày sinh</label> -->
                    <div class="flex1">
                      <date-mode-picker label="Ngày sinh" type="date"></date-mode-picker>
                    </div>

                    <div class="form-group">
                      <ms-input
                        label="Giới tính"
                        type="select"
                        v-model="form.gender"
                        placeholder="Chọn giới tính"
                        :options="gender"
                      />
                    </div>
                  </div>

                  <!-- Khu vực -->
                  <div class="form-group">
                    <ms-input
                      label="Khu vực"
                      type="select"
                      v-model="form.region"
                      placeholder="Chọn giá trị"
                      :options="[
                        { label: 'Nam', value: 'male' },
                        { label: 'Nữ', value: 'female' },
                      ]"
                    />
                  </div>

                  <!-- Số điện thoại + Email -->
                  <div class="form-row">
                    <ms-input
                      label="Số điện thoại"
                      name="fullName"
                      v-model="form.fullName"
                      placeholder="Nhập số điện thoại"
                      required
                    />

                    <ms-input
                      label="Email"
                      name="fullName"
                      v-model="form.fullName"
                      placeholder="Nhập email"
                      required
                    />
                  </div>

                  <!-- Địa chỉ -->
                  <ms-input
                    label="Địa chỉ"
                    name="fullName"
                    v-model="form.address"
                    placeholder="Nhập địa chỉ"
                    required
                  />

                  <!-- Học vấn -->
                  <h3 class="section-title">HỌC VẤN</h3>

                  <div class="form-group">
                    <div class="education-list">
                      <!-- Một dòng -->
                      <div class="edu-row">
                        <div class="left">
                          <div class="icon-dot"></div>
                          <span>Trình độ đào tạo</span>
                        </div>

                        <div class="input-wrapper">
                          <input type="text" class="dx-input" placeholder="Nhập trình độ đào tạo" />
                          <i class="fa-solid fa-plus icon-plus"></i>
                          <i class="fa-solid fa-chevron-down icon-dropdown-education"></i>
                        </div>
                      </div>

                      <!-- dòng 2 -->
                      <div class="edu-row">
                        <div class="left">
                          <div class="icon-dot"></div>
                          <span>Nơi đào tạo</span>
                        </div>

                        <div class="input-wrapper">
                          <input type="text" class="dx-input" placeholder="Nhập nơi đào tạo" />
                          <i class="fa-solid fa-plus icon-plus"></i>
                          <i class="fa-solid fa-chevron-down icon-dropdown-education"></i>
                        </div>
                      </div>

                      <!-- dòng 3 -->
                      <div class="edu-row">
                        <div class="left">
                          <div class="icon-dot"></div>
                          <span>Chuyên ngành</span>
                        </div>

                        <div class="input-wrapper">
                          <input type="text" class="dx-input" placeholder="Nhập chuyên ngành" />
                          <i class="fa-solid fa-plus icon-plus"></i>
                          <i class="fa-solid fa-chevron-down icon-dropdown-education"></i>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!--  THÊM HỌC VẤN  -->
                  <div class="add-title">+ Thêm học vấn</div>

                  <!--  HÀNG 1  -->
                  <div class="form-row">
                    <!-- Ngày ứng tuyển -->
                    <div class="flex1">
                      <date-mode-picker label="Ngày ứng tuyển " type="month"></date-mode-picker>
                    </div>

                    <!-- Nguồn ứng viên -->
                    <div class="form-group">
                      <ms-input
                        label="Nguồn ứng viên"
                        type="select"
                        v-model="form.region"
                        placeholder="Chọn giá trị"
                        :options="[
                          { label: 'Nam', value: 'male' },
                          { label: 'Nữ', value: 'female' },
                        ]"
                      />
                    </div>
                  </div>

                  <!--  HÀNG 2 -->
                  <div class="form-row">
                    <!-- Nhân sự khai thác -->
                    <div class="form-group">
                      <ms-input
                        label="Nhân sự khai thác"
                        type="select"
                        v-model="form.region"
                        placeholder="Chọn giá trị"
                        :options="[
                          { label: 'Nam', value: 'male' },
                          { label: 'Nữ', value: 'female' },
                        ]"
                      />
                    </div>

                    <!-- Cộng tác viên -->
                    <div class="form-group">
                      <ms-input
                        label="Cộng tác viên"
                        type="select"
                        v-model="form.region"
                        placeholder="Chọn nguồn ứng viên"
                        :options="[
                          { label: 'Nam', value: 'male' },
                          { label: 'Học sinh', value: 'female' },
                        ]"
                      />
                    </div>
                  </div>

                  <!-- ==================== CHECKBOX ==================== -->
                  <div class="checkbox-row">
                    <input type="checkbox" id="fastAdd" />
                    <label for="fastAdd" style="font-size: 14px; font-weight: 500; color: #374151"
                      >Thêm nhanh người tham chiếu vào kho ứng viên</label
                    >
                  </div>

                  <!-- ==================== THÊM NGƯỜI GIỚI THIỆU ==================== -->
                  <div class="add-title">+ Thêm người giới thiệu</div>

                  <!-- ==================== INPUT ==================== -->
                  <ms-input
                    label="Nơi làm việc gần đây"
                    name="fullName"
                    v-model="form.fullName"
                    placeholder="Nhập nơi làm việc gần đây"
                    required
                  />

                  <!-- ================== THÊM KINH NGHIỆM ================== -->
                  <hr class="divider-pop-up" />

                  <div class="add-title">+ Thêm kinh nghiệm làm việc</div>

                  <!-- Nơi làm việc -->
                  <ms-input
                    label="Nơi làm việc "
                    name="fullName"
                    v-model="form.fullName"
                    placeholder="Nhập nơi làm việc "
                    required
                  />

                  <!-- Thời gian -->
                  <div
                    class="form-row display-flex justify-content-space-between align-items-center"
                  >
                    <!-- Từ -->
                    <div class="flex1">
                      <date-mode-picker label="Thời gian " type="month"></date-mode-picker>
                    </div>

                    <!-- Đến -->
                    <div class="flex1">
                      <date-mode-picker label=". " type="month"></date-mode-picker>
                    </div>
                  </div>

                  <!-- Vị trí công việc -->
                  <ms-input
                    label="Vị trí công việc "
                    name="fullName"
                    v-model="form.fullName"
                    placeholder="Nhập vị trí công việc "
                    required
                  />

                  <!-- Mô tả -->
                  <div class="form-group">
                    <label class="label-input">Mô tả công việc</label>
                    <textarea class="dx-textarea" placeholder="Nhập mô tả công việc"></textarea>
                  </div>
                </div>
              </div>
            </a-form>
          </div>
        </div>

        <!-- BUTTON FOOTER -->
        <div class="modal-footer">
          <button type="button" class="btn-cancel">Hủy</button>
          <button type="submit" class="btn-save">Lưu</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Label */
.gender-item :deep(.ant-form-item-row) {
  display: flex !important;
  flex-direction: column !important;
  /* align-items: flex-start; */
}

/* Optional: chỉnh label nằm trên */
.gender-item :deep(.ant-form-item-label) {
  /* padding-bottom: 4px; */
  text-align: left !important;
  /* width: 100%; */
}
.gender-item :deep(.ant-form-item-label > label) {
  font-size: 14px;
  font-weight: 500;
  color: #374151;
}

.gender-item :deep(.ant-select-selector) {
  height: 36px !important;
  border-radius: 6px !important;
  padding-left: 12px !important;
}

.gender-item :deep(.ant-select-selection-placeholder) {
  color: #9ca3af !important;
}

/* Overlay */
/*  Ban đầu overlay sẽ hiển thị */
.overlay {
  position: fixed;
  /*  */

  inset: 0;
  background: #818283;
  /* Set up là none  */
  display: none;
  z-index: 1000;
  /* Làm mờ nền  */
  backdrop-filter: blur(2px);
  /*  độ ẩn trong suốt */
  opacity: 0.4;
  /* Làm hiệu ứng mượt */
  transition: opacity 0.3s ease;
}
/* Hiển thị overlay */
.overlay.show {
  display: block;
  z-index: 1000;
}
.modal {
  overflow: hidden;
  /* display: flex;
  flex-direction: column; */
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  box-shadow: 0px 8px 32px rgba(0, 0, 0, 0.12);
  border-radius: 8px;
  width: 560px;
  height: 660px;
  opacity: 0;
  pointer-events: none;
  /* background-color: gray; */
  /* Làm mượt hiệu ứng */
  transition:
    opacity 0.25s ease,
    transform 0.25s ease;
  z-index: 1000;
}

/* Khi modal mở */
.modal.show {
  opacity: 1;
  pointer-events: auto;
  transform: translate(-50%, -50%) scale(1);
}
/* ===== POPUP ADD (Override modal cũ) ===== */
.modal-content {
  flex: 1;
  overflow-y: auto;
}

.modal-add {
  /* width: 720px !important;
  max-height: 90vh !important; */
  border-radius: 8px;

  /* background: rgb(208, 90, 90); */
  /* display: flex;
  flex-direction: column; */
}

/* Header */
.modal-add .modal-header {
  position: sticky;
  top: 0;
  z-index: 10;
  background: white;
  /* padding: 16px 24px; */
  /* border-bottom: 1px solid #e5e7eb; */
  margin-left: 24px;
  margin-top: 24px;
  margin-right: 16px;
}
.modal-add .title-header {
  font-size: 24px;
  font-weight: 700;
  text-align: left;
}
.modal-content .modal-add .modal-header h2 {
  font-size: 24px;
  font-weight: 700;
  text-align: left;
}

/* Nút X */
.modal-add .icon-close {
  cursor: pointer;
  opacity: 0.7;
}

.modal-content-left {
  /* background-color: #394856; */
  height: 100%;
}
/* Upload CV */
.modal-add .upload-box {
  border: 0.8px dashed #d0d5dd !important;
  border-radius: 8px;
  padding: 30px !important;
  /* margin: 20px !important; */
  /* background: #fafafa; */
}

.modal-add .upload-box .title {
  font-size: 14px;
  font-weight: 600;
  color: #2e73f6;
}

.modal-add .upload-box .sub-title {
  font-size: 13px;
  color: #6b7280;
  margin-top: 8px;
}

/* Layout chính */
.modal-add .modal-content {
  /* display: flex; */
  padding: 24px 24px 24px 24px !important;
}
/* Content */
.modal-content-add {
  margin-top: 20px;
}

/* Avatar tròn */
.modal-add .avatar-box {
  width: 64px !important;
  height: 64px !important;
  border: 1px dashed #ced4da !important;
  border-radius: 50%;
  margin-top: 10px;
}

/* Form bên phải */
.modal-add .modal-content-right {
  background: white !important;
  padding-left: 20px;
  height: 100%;
}

.form-row {
  margin: 8px 0px;
}
.fa-calendar {
  font-size: 18px;
  color: rgb(107, 107, 107);
}
/* Label */
.modal-add .label-input {
  font-size: 14px;
  font-weight: 500;
  /* margin-bottom: 4px; */
  font-family: inherit;
}

/* Input  */

/* Sau thêm hover */
.modal-add select:focus,
.modal-add input:focus {
  border-color: #2680eb !important;
}

/* Ẩn placeholder option */
.modal-add select option[disabled] {
  color: #adb5bd;
}

/* Các dòng form */
.modal-add .row {
  display: flex;
  gap: 16px;
  margin-top: 12px;
}

/* Khu vực (dropdown) */
.modal-add .local select {
  width: 100%;
}

/* Footer */

/* Nút */

/* ===== Label ===== */
.label-input {
  font-size: 14px;
  color: #374151;
  font-family: inherit;
  /* background-color: #2680eb; */
  margin-bottom: 6px;
  display: block;
}
/* Chat GPT */
/* ===== Wrapper ===== */
.dx-input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  width: 100%;
}

/* ===== Input ===== */
.dx-input {
  width: 100%;
  height: 36px;
  padding: 8px 36px 8px 12px; /* chừa chỗ cho icon */
  border: 1px solid #d0d5dd; /* viền xám nhạt giống DevExpress */
  border-radius: 6px; /* bo góc chuẩn */
  font-size: 14px;
  background-color: white;
  transition: all 0.15s ease;
  outline: none;
  font-family: 'Inter', sans-serif;
  box-sizing: border-box;
}

/* Hover giống DX */
.dx-input:hover {
  border-color: #a6b0b9;
}

/* Focus giống DX */
.dx-input:focus {
  border-color: #4a90e2;
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.25);
}

/* ===== Icon ===== */
.dx-icon {
  /* Set up thành absolute icon */
  position: absolute;
  /* Icon luôn nằm bên phải */
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  color: #6b7280;
  font-size: 16px;
  pointer-events: none; /* để click vào icon vẫn focus input */
}
/* Chat GPT */
/* Font */

/* Container */
/* .form-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  /* gap: 16px; */
/* } */

/* Title */
.section-title {
  font-size: 14px;
  font-weight: 600;
  margin: 8px 0;
  color: #444;
}

/* Form Group */
.form-group {
  /* display: flex;
  flex-direction: column; */
  /* gap: 1px; */
}

/* Label */
.label-input {
  font-size: 14px;
  color: #374151;
}

.required {
  color: #e91e63;
}

/* 2 cột */
.form-row {
  display: flex;
  gap: 16px;
}

.form-row .form-group {
  flex: 1;
}

.dx-input {
  /* Bằng với chiều rộng của wrapper */
  width: 100%;
  height: 36px;
  padding: 8px 12px;
  padding-right: 36px; /* Tạo khoảng cách cho icon */
  border: 1px solid #d0d5dd;
  border-radius: 6px;
  font-size: 14px;
  background-color: #fff;
  outline: none;
  transition: all 0.15s ease;
  box-sizing: border-box;
}

.dx-input:hover {
  border-color: #a6b0b9;
}

.dx-input:focus {
  border-color: #4a90e2;
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.2);
}

/* Input wrapper */
/* .dx-input-wrapper {
  position: relative;
} */

/* Icon trong input */
.dx-icon {
  position: absolute;
  right: 10px;
  color: #6b7280;
  font-size: 16px;
  /* Căn giữa wrapper */
  top: 50%;
  /* Căn chỉnh giữa  */
  transform: translateY(-50%);
  pointer-events: none;
}

/* Select Style */
.dx-select {
  width: 100%;
  height: 36px;
  padding: 8px 12px;
  border: 1px solid #d0d5dd;
  border-radius: 6px;
  font-size: 14px;
  background-color: white;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg fill='gray' height='12' viewBox='0 0 24 24' width='12' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M7 10l5 5 5-5z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 12px center;
  outline: none;
  transition: 0.15s;
}

.dx-select:hover {
  border-color: #a6b0b9;
}

.dx-select:focus {
  border-color: #4a90e2;
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.2);
}
/* Education list */
.education-list {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

/* Mỗi dòng */
.edu-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Label trái */
.left {
  display: flex;
  align-items: center;
  gap: 8px;
  width: 170px; /* để cố định khoảng cách */
}

.icon-dot {
  width: 5px;
  height: 5px;
  background: #6b7280;
  border-radius: 50%;
}

/* Bọc input */
.input-wrapper {
  position: relative;
  /* max-width: 420px; */
  flex: 1;
}

/* Input */
.dx-input {
  width: 100%;
  height: 36px;
  padding: 8px 60px 8px 14px; /* CHỪA CHỖ CHO 2 ICON */
  border: 1px solid #d0d5dd;
  border-radius: 6px;
}

/* Icon dấu cộng */
.icon-plus {
  position: absolute;
  right: 38px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 14px;
  color: #2680eb;
  cursor: pointer;
}

/* Icon dropdown */
.icon-dropdown-education {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 14px;
  color: #6b7280;
  cursor: pointer;
}

/* Thêm học vấn */
.add-title {
  color: #2680eb;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  margin: 8px 0 4px 0;
}

.form-row {
  display: flex;
  gap: 20px;
  margin: 12px 0;
}

.form-row .form-group {
  flex: 1;
}

.checkbox-row {
  display: flex;
  align-items: center;
  gap: 8px;
  margin: 12px 0;
  font-size: 14px;
}

/* Input wrapper */
.dx-input-wrapper {
  position: relative;
  width: 100%;
}

/* Input */
.dx-input {
  width: 100%;
  height: 36px;
  padding: 8px 12px;
  padding-right: 36px;
  border: 1px solid #d0d5dd;
  border-radius: 6px;
  font-size: 14px;
  background: white;
  outline: none;
  transition: 0.15s;
}

.dx-input:focus {
  border-color: #2680eb;
  box-shadow: 0 0 0 3px rgba(38, 128, 235, 0.2);
}

/* Icon trong input */
.dx-icon {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  color: #6b7280;
  pointer-events: none;
  font-size: 16px;
}

/* Select */
.dx-select {
  width: 100%;
  height: 36px;
  padding: 8px 12px;
  border: 1px solid #d0d5dd;
  border-radius: 6px;
  font-size: 14px;
  background-color: white;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg fill='gray' height='12' viewBox='0 0 24 24' width='12' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M7 10l5 5 5-5z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 12px center;
}

.dx-select:focus {
  border-color: #2680eb;
  box-shadow: 0 0 0 3px rgba(38, 128, 235, 0.2);
}
.add-title {
  color: #2680eb;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  margin: 12px 0 6px 0;
}

.checkbox-row {
  display: flex;
  align-items: center;
  gap: 8px;
  margin: 12px 0;
}
.add-title {
  color: #2680eb;
  font-size: 14px;
  margin: 12px 0;
  cursor: pointer;
}

.divider-pop-up {
  margin: 18px 0;
  border: none;
  border-top: 1px solid #e5e7eb;
}

/* TEXTAREA */
.dx-textarea {
  width: 100%;
  height: 90px;
  padding: 10px 14px;
  border: 1px solid #d0d5dd;
  border-radius: 6px;
  font-size: 14px;
  resize: none;
  box-sizing: border-box;
}

/* Input icon */
.input-wrapper {
  position: relative;
}

.input-icon {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  color: #6b7280;
  pointer-events: none;
}
.modal-footer {
  display: flex;
  background-color: #f1f2f5;
  justify-content: flex-end;
  gap: 14px;
  padding-left: 24px;
  padding-right: 24px;
  padding-top: 9px;
  padding-bottom: 9px;
  margin-top: 20px;

  position: sticky;
  bottom: 0;
  z-index: 10;
  /* background: white; */
  border-top: 1px solid #e5e7eb;
}

.btn-cancel {
  padding: 8px 22px;
  background: #f3f4f6;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
}

.btn-cancel:hover {
  background: #e5e7eb;
}

.btn-save {
  padding: 8px 26px;
  background: #1e88e5;
  border: none;
  border-radius: 6px;
  color: white;
  font-size: 14px;
  cursor: pointer;
}

.btn-save:hover {
  background: #1876c7;
}
</style>
