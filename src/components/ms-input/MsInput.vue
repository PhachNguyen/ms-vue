<script setup>
// Nhận model từ cha dùng v-model
const model = defineModel()
//  Khai báo props
const props = defineProps({
  label: String,
  placeholder: String,
  type: { type: String, default: 'text' },
  required: Boolean,
})
</script>
<template>
  <!-- <div class="display-flex flex-column">

    <label for="" class="label-input"> {{ label }}</label>
    <input
    :typle="type"
    :placeholder="placeholder"
    class="dx-input"
    v-model="model"
    >
    </input>

  </div> -->
  <div class="form-group display-flex flex-column">
    <label class="label-input">{{ label }} <span class="required">*</span></label>
    <input v-if="type !== 'select'" :type="text" class="dx-input" :placeholder="placeholder" />
  </div>
</template>

<style>
.form-group {
  /* display: flex;
  flex-direction: column; */
  /* gap: 1px; */
}

/* Label */
.label-input {
  font-size: 14px;
  font-weight: 500;
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
</style>
