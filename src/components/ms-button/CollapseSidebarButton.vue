<script setup>
//  Định nghĩa một emit truyền lên cha
const emit = defineEmits(['collapsed'])
//  Hàm emit
function handleClickCollapse() {
  // debugger

  emit('collapsed')
}
</script>

<template>
  <!-- Button thu gọn -->
  <div class="close display-flex justify-content-center align-items-flex-end flex-row">
    <button
      class="btn-close-sidebar display-flex justify-content-start align-items-center flex-row"
      @click="handleClickCollapse"
    >
      <div class="icon-btn-close"></div>
      <span class="name-btn-close">Thu gọn</span>
    </button>
  </div>
</template>

<style scoped>
.sidebar .btn-close-sidebar {
  background-color: #1d2734;
  width: 193px;
  height: 32px;
  padding: 20px;
  /* text-align: left; */
  display: flex;
  /* align-items: flex-end; */

  gap: 12px;
  /* background-color: #394856; */
  border: none;
  border-radius: 6px;
  color: #c5cccb;
  font-size: 14px;
  cursor: pointer;
}
/* Thu gọn */
.sidebar.collapsed .btn-close-sidebar {
  padding-left: 0;
  padding-right: 0;
  width: 45px;
}
</style>
