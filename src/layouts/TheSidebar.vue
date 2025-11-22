<script setup>
import CollapseSidebarButton from '@/components/ms-button/CollapseSidebarButton.vue'
import MsButton from '@/components/ms-button/MsButton.vue'
import { ref } from 'vue'

const isCollapsed = ref(false)
function Toggle() {
  // debugger
  isCollapsed.value = !isCollapsed.value
}
</script>
<template>
  <!-- Sidebar -->
  <div class="sidebar display-flex flex-column" :class="{ collapsed: isCollapsed }">
    <div class="sidebar-item">
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-newpaper"></div>
        <h2 class="name">Tin tuyển dụng</h2>
      </div>
      <div
        class="line display-flex align-items-center flex-row"
        style="
          background-color: #2680eb;

          border-radius: 5px;
        "
      >
        <div class="icon-user-2"></div>
        <h2 class="name" id="pick-sidebar">Ứng viên</h2>
      </div>

      <div class="line display-flex align-items-center flex-row">
        <div class="icon-calendar"></div>
        <h2 class="name">Lịch</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-warehouse"></div>
        <h2 class="name">Kho tiềm năng</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-markerting"></div>
        <h2 class="name">Chiến dịch tuyển dụng</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-job"></div>
        <h2 class="name">Công việc</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-mail"></div>
        <h2 class="name">aiMarketing</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-chat-sidebar"></div>
        <h2 class="name">Trao đổi ứng viên</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-report"></div>
        <h2 class="name">Báo cáo</h2>
      </div>
      <div class="line display-flex align-items-center flex-row">
        <div class="icon-other"></div>
        <h2 class="name">Khác</h2>
      </div>
    </div>
    <MsButton type="collapse" label="Thu gọn" icon="icon-btn-close" @collapse="Toggle"></MsButton>
    <!-- <collapse-sidebar-button @collapsed="Toggle"></collapse-sidebar-button> -->
  </div>
</template>
<style>
.sidebar {
  width: 233px;
  height: 100%;
  background-color: #030f1d;
  padding-top: 32px;
  padding-bottom: 16px;
}
.sidebar-item {
  /* display: flex;
  text-align: center;
  justify-content: center;
  align-items: center; */
  margin-bottom: 40px;
}
.line {
  height: 24px;
  /* background-color: #394856; */
  padding: 8px 12px;
  margin: 0 12px 12px 12px;
}
.sidebar .name {
  color: #c5cccb;
  line-height: 21px;
  font-size: 14px;
  font-weight: 500;
  text-align: left;
  /* margin: 16px 0; */
  margin-left: 12px;
  /* padding: 8px 12px; */
  /* border-radius: 6px; */
  cursor: pointer;
}
/* .sidebar .close{
    position: relative;
    width: 100%;
}
.sidebar .icon-btn-close {
    position: absolute;
    left: 40px;
    top: 50%;

    padding-right: 8px;

} */
/* .sidebar .close{
    display: flex;
    justify-content: center;
    align-items: flex-end;
 } */

/*  Thu gọn sidebar */
.sidebar.collapsed {
  width: 70px;
  transition: 0.2s ease;
}
/*  Ẩn chữ  */
.sidebar.collapsed .name,
.sidebar.collapsed .name-btn-close {
  display: none;
}
/* Icon căn giữa */
.sidebar.collapsed .line,
.sidebar.collapsed .btn-close-sidebar {
  justify-content: center;
}

.sidebar.collapsed .btn-close-sidebar {
  padding-left: 0;
  padding-right: 0;
  width: 45px;
}

/* Xoay icon thu gọn */
.sidebar.collapsed .icon-btn-close {
  transform: rotate(180deg);
  transition: 0.2s;
}
</style>
