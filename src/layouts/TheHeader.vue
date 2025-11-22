<template>
  <div class="header display-flex justify-content-space-between align-items-center flex-row">
    <!-- <h1>Tuyển dụng</h1> -->
    <!-- Header left -->
    <div class="header-left display-flex align-items-center flex-row">
      <div class="icon-menu"></div>
      <div class="logo"></div>
      <h2 class="header-name-right">Tuyển dụng</h2>

      <!-- Nội dung bên trái của header -->
    </div>
    <!-- Header center -->
    <div class="header-center display-flex align-items-center flex-row">
      <div class="search-box">
        <div class="icon-search"></div>
        <input
          type="text"
          class="title-search"
          placeholder="Tìm kiếm tin tuyển dụng, ứng viên, nhân tài ..."
        />
      </div>
    </div>
    <!-- Header right -->
    <div class="header-right display-flex align-items-center flex-row justify-content-flex-end">
      <div class="icon-website"></div>
      <!-- Nội dung bên phải của header -->
      <h2 class="header-name-left">Website tuyển dụng</h2>
      <div class="icon-sound"></div>
      <div class="icon-store"></div>
      <div class="icon-user"></div>
      <div class="icon-chat"></div>
      <div class="icon-noti"></div>
      <div class="icon-help"></div>
      <div class="icon-setting"></div>
      <div class="icon-help2"></div>
      <div class="avatar-img"></div>
    </div>
  </div>
</template>
<style scoped>
.header {
  /* background-color: white; */
  height: 48px;
  border-bottom: 1px solid gray;
  /* padding: 16px;
    text-align: flex-start; */
}
.content {
  /* padding: 16px; */
  background-color: white;
}
.header .icon-menu {
  margin-left: 15px;
}
.logo {
  /* margin-left: 10px; */
}
.logo-img {
  background-image: url(../icons/logo.svg);
  background-repeat: no-repeat;

  width: 32px;
  height: 32px;
  margin: 0;
  background-size: contain;
}
.sidebar {
  width: 250px;
  height: 100%;
  background-color: #030f1d;
  padding-top: 32px;
  padding-bottom: 16px;
}

.header .header-right {
  /* float: right; */
  /* background-color: lightpink; */
  width: calc(100% - 500px);
  padding-right: 14px;
  height: 100%;
}
.header .header-name-right {
  /* margin-left: 12px; */
  margin-right: 24px;
  font-size: 18px;
  font-weight: 700;
  text-align: left;

  /* width: auto;
    height: auto; */
  font-family: inherit;
}
/* Header center */
.header .header-center {
  /* float: left; */
  /* background-color: lightblue; */
  width: calc(100% - 500px - 200px);
  height: 100%;
}

.search-box {
  /*  Set up position  */
  position: relative;
  width: 420px;
}

.icon-search {
  position: absolute;
  left: 10px;
  top: 50%;
  transform: translateY(-50%);
  padding-right: 8px;
  opacity: 0.7;
}

.title-search {
  width: 100%;
  padding: 8px 12px 8px 34px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
  outline: none;
}

/* Header left */
.header .header-left {
  /* float: left; */
  /* background-color: lightgreen; */
  width: 400px;

  height: 100%;
}
.header .header-name-left {
  margin-right: 12px;
  /* margin-left: 24px; */
  font-size: 14px;
  font-weight: 300px;
  text-align: left;
  font-family: inherit;

  /* width: auto;
    height: auto; */
}
</style>
