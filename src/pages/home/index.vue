<template>
  <div>
    <div class="list">
      <div
        class="banner"
        v-for="(item,index) in data.list"
        :key="index"
        :id="item.id"
        @click="bindList(item.name)"
      >
        <div class="list-img">
          <img :src="item.img" alt>
        </div>
        <div class="list-val">{{item.name}}</div>
      </div>
    </div>

    <div class="kind">
      <dl>
        <dt>
          <img :src="kindImg" alt @click="bindImg">
        </dt>
        <dd>
          <p>{{kindName}}</p>
          <p>{{label}}</p>
        </dd>
        <dd>
          <span class="kind-right" @click="kindClick(kindName)">></span>
        </dd>
      </dl>
    </div>
    <!-- <div class="footer">
      <span v-for="(item,index) in data.arr" :key="index">{{item.name}}</span>
    </div> -->
    <div class="swiper">
      <swiper class="vvs">
        <swiper-item v-for="(v,i) in find.swipers" :key="i" @click="swiperImg(v.title,v.write)">
          <img :src="v.img" alt class="swiper-img">
          <h4>{{v.title}}</h4>
        </swiper-item>
      </swiper>
    </div>
    <div class="end">
      <span></span>
      <b>特别推荐</b>
      <span></span>
    </div>
    <div class="content">
      <dl v-for="(item,ind) in arr" :key="ind" @click="bindCont(ind)">
        <dt>
          <img :src="item.img" alt>
        </dt>
        <dd>
          <p>{{item.title}}</p>
          <span>{{item.cate}}</span>
        </dd>
      </dl>
    </div>
    <div class="end">
      <span></span>
      <b>精彩文章</b>
      <span></span>
    </div>
    <div class="content">
      <dl v-for="(item,ind) in list" :key="ind">
        <dt>
          <img :src="item.img" alt>
        </dt>
        <dd>
          <p>{{item.title}}</p>
          <span>{{item.cate}}</span>
        </dd>
      </dl>
    </div>
    <div class="hide" v-if="flag">
      <div
        class="hides"
        v-for="(item,index) in data.list"
        :key="index"
        :id="item.id"
        @click="hideBind(item)"
      >
        <div class="list-img">
          <img :src="item.img" alt>
        </div>
        <div class="list-val">{{item.name}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import data from "../../data/head"; //十二条星座的数据
import find from "../../data/find"; //图片轮播点击对应得数据
export default {
  data() {
    return {
      data, //十二条星座的数据
      find, //图片轮播点击对应得数据
      date: "2016-09-01",
      arr: [], //特别推荐数据
      list: [], //精彩文章
      val: "", //星座名
      flag: false,
      kindImg: "",
      kindName: "",
      label: ""
    };
  },
  methods: {
    //头部每一项点击跳转显示的对应数据
    bindList(val) {
      this.val = val;
      wx.navigateTo({
        url: "/pages/recommend/main?name=" + val
      });
    },
    //点击kind的图片显示
    bindImg() {
      this.flag = true;
    },
    //点击kind的图片显示后， 随机选择选中后bingImg隐藏
    hideBind(arr) {
      this.kindImg = arr.img;
      this.kindName = arr.name;
      this.label = arr.desc;
      this.flag = false;
    },
    //点击箭头跳转
    kindClick(mz) {
      wx.navigateTo({
        url: "/pages/content/main?name=" + mz
      });
    },
    //图片轮播点击跳转
    swiperImg(tit, write) {
      wx.navigateTo({
        url: "/pages/swiper/main?name=" + tit + "&write=" + write,
      });
    },
    //点击特别推荐列表跳转页面
    bindCont() {
      wx.navigateTo({
        url: "/pages/list/main"
      });
    }
  },
  //接口
  created() {
    wx.request({
      url: "https://m.xzw.com/apidat/article/2.js?cp=5CF0A78C796069F",
      success: result => {
        this.arr = result.data;
      }
    });
    wx.request({
      url: "https://m.xzw.com/apidat/article/3.js?cp=5CF0A78C796069F",
      success: result => {
        this.list = result.data;
      }
    });
  }
};
</script>

<style>
.swiper-img {
  width: 80%;
  height: 80%;
  margin-left: 10%;
}
h4 {
  margin-left: 10%;
  height: 80rpx;
  line-height: 80rpx;
}
.swiper {
  width: 100%;
  height: 500rpx;
}
.vvs {
  height: 500rpx;
}
.hide {
  position: absolute;
  top: 185rpx;
  left: 0;
  width: 100%;
  height: 1000rpx;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  background: #ccc;
}
.hides {
  width: 30%;
  height: 260rpx;
}
.kind-right {
  font-size: 50rpx;
  margin-left: 50rpx;
}
.list {
  width: 100%;
  height: 160px;
  display: flex;
  overflow: hidden;
  white-space: nowrap;
  overflow-x: scroll;
  flex-shrink: 0;
  flex-wrap: nowrap;
}
.banner {
  width: 22%;
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.list-img {
  width: 180rpx;
  height: 180rpx;
  display: flex;
  justify-content: center;
}
.list-img img {
  width: 100%;
  height: 100%;
}
.kind {
  width: 100%;
  height: 200rpx;
}
dl {
  width: 100%;
  height: 200rpx;
  display: flex;
}
dt {
  width: 30%;
  height: 200rpx;
}
dt img {
  width: 100%;
  height: 100%;
}
dd {
  height: 200rpx;
  margin-left: 20rpx;
}
dd p {
  height: 60rpx;
  line-height: 60rpx;
}

.footer {
  width: 100%;
  height: 60rpx;
  display: flex;
  justify-content: space-around;
  margin-top: 30rpx;
}
.end {
  width: 100%;
  height: 100rpx;
  line-height: 100rpx;
  color: blueviolet;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.end span {
  width: 200rpx;
  height: 3rpx;
  border: solid 1px #ccc;
  background: #ccc;
}
.end b {
  font-size: 40rpx;
}
.content dl {
  margin: 30rpx 0;
}
.content dl dd p {
  height: 100rpx;
}
.content dl dd span {
  color: orange;
}
</style>
