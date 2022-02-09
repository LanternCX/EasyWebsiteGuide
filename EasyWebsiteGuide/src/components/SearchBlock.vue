// 搜索框组件 默认百度搜索
<template>
  <div id='search'>
    <form
      action="https://www.baidu.com/s"
      id="form"
    >
      <input
        type="text"
        name="wd"
        placeholder="在此进行搜索..."
        class="searchInput"
        autocomplete="off"
      >
      <span
        class="searchBtn"
        @click="formSubmit()"
      >
        <img
          type="submit"
          src="@/assets/search.svg"
          width="30px"
          height="30px"
          class="icon"
        >
      </span>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SearchBlock',
  methods: {
    //搜索按钮功能：提交
    formSubmit() {
      document.getElementById("form").submit();
    }
  }
}
</script>

<style scoped>
#search {
  position: absolute;
  width: 100%;
  margin: auto;
  top: 150px;
  text-align: center;
}

#form {
  margin-right: 80px;
}

.searchInput {
  all: initial;
  height: 50px;
  width: 30%;
  opacity: 0.7;
  background-color: #2f3640;
  border-style: none;
  border-radius: 150px;
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;
  color: #f4f4f4;
  font-family: 楷体;
  font-size: large;
  text-align: center;
  transition-duration: 0.5s;
}
.searchInput:hover {
  opacity: 0.95;
  box-shadow: 0 10px 50px 0px rgba(1, 1, 1);
  width: 60%;
}
.searchInput:focus {
  opacity: 1;
  background-color: #7f8c8d;
  box-shadow: 0 10px 50px 0px rgba(1, 1, 1);
  width: 60%;
}
.searchInput:focus::placeholder {
  color: #7f8c8d;
}

.searchBtn {
  position: absolute;
  height: 50px;
  width: 70px;
  border-style: none;
  opacity: 0.7;
  border-radius: 150px;
  border-top-left-radius: 0px;
  border-bottom-left-radius: 0px;
  background-color: #2f3640;
  color: #f4f4f4;
  transition-duration: 0.5s;
}
.searchBtn:hover {
  box-shadow: 0 10px 50px 0px rgba(1, 1, 1);
  opacity: 0.95;
}

.icon {
  margin-top: 12px;
  margin-left: 3px;
}
</style>
