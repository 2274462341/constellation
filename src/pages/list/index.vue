<template>
  <div>
    <h4>笑吧 笑吧</h4>
    <div>
      <scroll-view
        scroll-y="true"
        class="scroll"
        upper-threshold="350"
        lower-threshold="350"
        bindscrolltoupper="aaa"
        bindscrolltolower="ccc"
        bindscroll="scrolllistener"
      >
        <p v-for="(item,index) in arr" :key="index">{{item.content}}</p>
      </scroll-view>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr: [], //接口数据
      page:0,
      pagesize:10
    };
  },
  methods: {
   
  },
  onPullDownRefresh()
  {
 wx.request({
      url:
        "http://v.juhe.cn/joke/content/text.php?key=11ccc6e75382ddfe642fb64955301946&page=1&pagesize=10",
      data: {
        page: this.page,
        pagesize: this.pagesize
      },
      success: result => {
        console.log(result.data.result.data);
        this.arr = result.data.result.data;
      }
    });
  },
   onReachBottom() {
    // 上拉加载更多
     wx.request({
      url:
        "http://v.juhe.cn/joke/content/text.php?key=11ccc6e75382ddfe642fb64955301946&page=1&pagesize=10",
      data: {
        page: this.page,
        pagesize: this.pagesize+5
      },
      success: result => {
        console.log(result.data.result.data);
        this.arr = result.data.result.data;
      }
    });
 
  },
  created() {
   wx.request({
      url:
        "http://v.juhe.cn/joke/content/text.php?key=11ccc6e75382ddfe642fb64955301946&page=1&pagesize=5",
      data: {
        page: 1,
        pagesize: 5
      },
      success: result => {
        console.log(result.data.result.data);
        this.arr = result.data.result.data;
      }
    });
  }
};
</script>

<style>
h4 span {
  font-size: 30rpx;
}
h4 {
  text-align: center;
}
</style>
