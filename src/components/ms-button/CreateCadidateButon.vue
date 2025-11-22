<template>
  <!-- Gọi sự kiện emit -->
  <div
    class="btn-create-new display-flex justify-content-center align-items-center flex-row"
    @click="handleClick"
  >
    <!-- <button class="btn-create-new-candidate">  -->
    <div class="icon-plus"></div>
    <span class="title-btn-create-new">Thêm ứng viên</span>
    <!-- <button onclick="openModal()">+ Thêm ứng viên</button> -->

    <div class="divider"></div>
    <div class="icon-dropdown"></div>
    <!-- </button> -->
  </div>
</template>
<style scoped>
.btn-create-new {
  background-color: #2680eb;
  /* width: 128px; */
  height: 19px;
  padding: 8px 12px;
  gap: 8px;
  margin-left: 15px;
  cursor: pointer;
}
.btn-create-new .title-btn-create-new {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-right: 12px;
  padding-left: 12px;
  border-top-width: 0, 8;
  /* background-color: #2680EB; */
  padding-left: 8px;
  font-size: 14px;
  color: white;
  font-weight: 500;
  /* width: 100%;
    height: 100%; */
}
.divider {
  width: 0.1px;
  height: 36px;
  background: black;

  margin: 0 6px;
}
.btn-create-new .icon-dropdown {
  /* border-left: #394856 1px solid; */
  padding-left: 8px;
}
</style>
<script setup>
//  Nút nhiệm vụ emit một sự kiện khi click
//  Tạo sự kiện click của button
const emit = defineEmits(['click'])
//  Function click
//  = > Đã truyền được lên main content
function handleClick() {
  console.log('Function đã hoạt động ở button')
  emit('click')
}
</script>
