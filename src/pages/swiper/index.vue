<template>
  <div>
    <div class="header">{{name}}</div>
    <div class="gray">{{write}}</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "", //标题名字
      write: "" //标题文章
    };
  },
  onLoad(e) {
    this.name = e.name;
    this.write = e.write;
  }
};
</script>
<style>
.header {
  width: 100%;
  height: 100rpx;
  line-height: 100rpx;
  text-align: center;
  color: #e77099;
  font-weight: bolder;
}
.gray {
  width: 90%;
  margin-left: 5%;
  height: 600rpx;
  background: #f6f6f6;
  line-height: 80rpx;
  text-indent: 2em;
}
</style>
