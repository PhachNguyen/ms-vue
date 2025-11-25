<script setup>
import TableCandidate from '@/views/TableCandidate.vue'
import CreateCadidateButon from '@/components/ms-button/CreateCadidateButon.vue'
import AddCandidate from '@/views/AddCandidate.vue'
import MsButton from '@/components/ms-button/MsButton.vue'
import Form from '@/views/PopupCandidate.vue'

import { onMounted, ref, watch } from 'vue'

import PopupCandidate from '@/views/PopupCandidate.vue'

//  Set up ban đầu là flase
const isOpen = ref(false)
const rows = ref([])

//  Debugger
// Done
onMounted(() => {
  rows.value = JSON.parse(localStorage.getItem('candidateList') || '[]')
})
function debugClick() {
  console.log('MainContent : đã nhận')
}
function loadData() {
  debugger

  rows.value = JSON.parse(localStorage.getItem('candidateList') || '[]')
  // debugger
  // console.log('Giá trị ' + rows.value)
}

// watch(rows, (value) => {
//   loadData()
// })
</script>
<template>
  <!-- Content -->
  <div class="main-content flex1 display-flex flex-column">
    <PopupCandidate v-model="isOpen" @reload="loadData" />
    <div
      class="main-content-header display-flex justify-content-space-between align-items-center flex-row"
    >
      <h2>Ứng viên</h2>
      <!-- <create-cadidate-buton @click="isOpen = true"></create-cadidate-buton> -->
      <div class="btn-create-box">
        <MsButton type="add" icon="icon-plus" label="Thêm ứng viên" @click="isOpen = true" />
        <MsButton type="add" icon="icon-dropdown" class="btn-dropdown" />
      </div>

      <!-- <h1>Trạng thái isOpen là : {{ isOpen }}</h1> -->
    </div>
    <!-- Header-main content -->
    <!-- Main-content search -->
    <div
      class="main-content-search display-flex justify-content-space-between align-items-center flex-row"
    >
      <div class="btn-search">
        <div class="icon-ai-search"></div>
        <input type="text" class="title-search" placeholder="Tìm kiếm hoặc nhờ AI trợ giúp" />
      </div>
      <div class="search-right display-flex justify-content-space-between">
        <div class="search-icon">
          <div class="icon-filter"></div>
        </div>
        <div class="search-icon">
          <div class="icon-toolbar"></div>
        </div>
        <div class="search-icon">
          <div class="icon-check"></div>
        </div>
        <div class="search-icon">
          <div class="icon-setting-2"></div>
        </div>
      </div>
    </div>

    <!-- Table -->
    <TableCandidate :rows="rows"></TableCandidate>

    <!-- Content bottom -->
  </div>
</template>

<style scoped>
.main-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow: hidden;
}

.main-content-header {
  /* font-size: 24px;
    font-weight: 700;
    margin-bottom: 24px;
    width: 100%; */
  padding: 16px 24px 0 24px;
  /* background-color: turquoise; */
}

.main-content-search {
  margin-top: 5px;
  height: 48px;
  /* background-color: yellow; */
}
.btn-search {
  padding: 16px;
  position: relative;
  height: 85%;
  /* width: 1236px; */
}
.main-content-search .icon-ai-search {
  position: absolute;
  left: 30px;
  top: 45%;
  transform: translateY(-50%);
  padding-right: 16px;
  opacity: 0.7;
}
.main-content-search .title-search {
  width: 100%;
  padding: 8px 12px 8px 45px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
  outline: none;
}
.search-right {
  width: 15%;
  margin-right: 15px;
}

.btn-create-box {
  display: inline-flex;
}

.btn-create-box .ms-btn--add {
  border-radius: 6px 0 0 6px;
}

.btn-create-box .btn-dropdown {
  border-left: 1px solid rgba(255, 255, 255, 0.4);
  border-radius: 0 6px 6px 0;
  padding-left: 12px;
  padding-right: 12px;
}
/* Hiệu ứng hover cho nút add */
.btn-create-box .ms-btn--add:hover {
  background-color: #4097ff; /* xanh đậm hơn */
  transition: 0.15s ease-in-out;
}

/* Hover cho nút dropdown */
.btn-create-box .btn-dropdown:hover {
  background-color: #4097ff;
  border-left-color: rgba(255, 255, 255, 0.6);
  transition: 0.15s ease-in-out;
}

/* Icon + text hover (cho đẹp hơn) */
.btn-create-box .ms-btn-label,
.btn-create-box .icon {
  transition: 0.12s ease;
}

.btn-create-box .ms-btn--add:hover .ms-btn-label,
.btn-create-box .btn-dropdown:hover .icon {
  filter: brightness(1.15);
}
</style>
