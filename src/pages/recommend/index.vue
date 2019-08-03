<template>
  <div class="section-two">
    <div class="tab">
      <span
        :class="currentTab==item.id?'nav active': 'nav'"
        v-for="(item,index) in list"
        :key="index"
        @click="bindCurent(item.id)"
      >{{item.name}}</span>
    </div>
    <swiper class="cont" :current="currentTab" circular="true" skip-hidden-item-layout="true">
      <!-- todays -->
      <swiper-item>
        <div class="todays">
          <p>{{todayArr.name}}</p>
          <div calss="date">{{todayArr.datetime}}</div>
          <div class="sum">{{todayArr.summary}}</div>
          <div class="Qc">
            <span>速配星座：{{todayArr.QFriend}}</span>
            <span>幸运色：{{todayArr.color}}</span>
          </div>
           <canvas id="canvas_circle" width="300" height="600" ></canvas>
          <div class="zhi">
            <span>综合指数：{{todayArr.all}}</span>
            <span>爱情指数：{{todayArr.love}}</span>
            <span>财运指数：{{todayArr.money}}</span>
            <span>健康指数：{{todayArr.health}}</span>
            <span>事业指数：{{todayArr.work}}</span>
          </div>
        </div>
      </swiper-item>
      <!-- tomorrows -->
      <swiper-item>
        <div class="tomorrows">
          <p>{{tomorrowArr.name}}</p>
          <div calss="date">{{tomorrowArr.datetime}}</div>
          <div class="sum">{{tomorrowArr.summary}}</div>
          <div class="Qc">
            <span>{{tomorrowArr.QFriend}}</span>
            <span>{{tomorrowArr.color}}</span>
          </div>
          <div class="zhi">
            <span>综合指数：{{tomorrowArr.all}}</span>
            <span>爱情指数：{{tomorrowArr.love}}</span>
            <span>财运指数：{{tomorrowArr.money}}</span>
            <span>健康指数：{{tomorrowArr.health}}</span>
            <span>事业指数：{{tomorrowArr.work}}</span>
          </div>
        </div>
      </swiper-item>
      <!-- weeks -->
      <swiper-item>
        <div class="weeks">
          <p>{{weekArr.name}}</p>
          <div calss="date">{{weekArr.date}}</div>
          <div class="zhi">
            <span>爱情指数：{{weekArr.love}}</span>
            <span>财运指数：{{weekArr.money}}</span>
            <span>事业指数：{{weekArr.work}}</span>
          </div>
        </div>
      </swiper-item>
      <!-- nextweeks -->
      <swiper-item>
        <div class="nextweeks">
          <p>{{nextweekArr.name}}</p>
          <div calss="date">{{nextweekArr.date}}</div>
          <div class="zhi">
            <span>爱情指数：{{nextweekArr.love}}</span>
            <span>财运指数：{{nextweekArr.money}}</span>
            <span>事业指数：{{nextweekArr.work}}</span>
          </div>
        </div>
      </swiper-item>
      <!-- months -->
      <swiper-item>
        <div class="months">
          <p>{{monthArr.name}}</p>
          <div calss="date">{{monthArr.date}}</div>
          <div class="Qc">
            <b>happy:</b>
            <span>{{monthArr.happyMagic}}</span>
          </div>
          <div class="zhi">
            <span>综合指数：{{monthArr.all}}</span>
            <span>爱情指数：{{monthArr.love}}</span>
            <span>财运指数：{{monthArr.money}}</span>
            <span>健康指数：{{monthArr.health}}</span>
            <span>事业指数：{{monthArr.work}}</span>
          </div>
        </div>
      </swiper-item>
      <!-- year -->
      <swiper-item>
        <div class="years">
          <p>{{yearArr.name}}</p>
          <div class="Qc">
            <b>幸运物：</b>
            <span>{{yearArr.luckeyStone}}</span>
          </div>
          <div class="zhi">
            <b>爱情指数：</b>
            <span>{{yearArr.love}}</span>
            <b>财运指数 ：</b>
            <span>{{yearArr.finance}}</span>
            <b>健康指数：</b>
            <span>{{yearArr.health}}</span>
            <b>事业指数：</b>
            <span>{{yearArr.career}}</span>
          </div>
        </div>
      </swiper-item>
    </swiper>
  </div>
</template>

<script>

export default {


  data() {
    return {
      currentTab: "0",
      list: [
        { name: "今天", id: 0 },
        { name: "明天", id: 1 },
        { name: "本周", id: 2 },
        { name: "下周", id: 3 },
        { name: "本月", id: 4 },
        { name: "今年", id: 5 }
      ],
      val: "", //接收的name
      todayArr: {}, //today的数据
      tomorrowArr: {}, //tomorrowArr的数据
      weekArr: {}, //weekArr的数据
      nextweekArr: {}, //nextweekArr的数据
      monthArr: {}, //monthArr的数据
      yearArr: {} //yearArr的数据
    };
  },
  methods: {
    bindCurent: function(res) {
      this.currentTab = res;
    }
  },
  onLoad(options) {
    this.val = options.name;
    wx.request({
      url:
        "http://web.juhe.cn:8080/constellation/getAll?key=f0c93a2f51f2a010953f9b947bf130ca",
      data: {
        consName: this.val
      },
      method: "GET",
      success: result => {
        this.todayArr = result.data.today;
        this.tomorrowArr = result.data.tomorrow;
        this.weekArr = result.data.week;
        this.nextweekArr = result.data.nextweek;
        this.monthArr = result.data.month;
        this.yearArr = result.data.year;
      }
    });
  }
};
</script>

<style>
/*第二功能模块*/
.section-two {
  width: 100%;
  height: auto;
  overflow: hidden;
  background-color: #fff;
  display: flex;
}
/*轮播图导航 */
.tab {
  width: 20%;
  height: 1000rpx;
  box-sizing: border-box;
  padding: 20rpx 0 20rpx;
  display: flex;
  flex-direction: column;
  /* align-items: center; */
  border-bottom: 1rpx solid #ebebeb;
  position: fixed;
}
.tab span {
  height: 100rpx;
  line-height: 100rpx;
  font-size: 38rpx;
}
.nav {
  text-align: center;
  flex: 1;
  font-weight: 600;
  box-sizing: border-box;
}
.nav:nth-of-type(odd) {
  border-left: 1rpx solid #ebebeb;
  border-right: 1rpx solid #ebebeb;
}
.nav.active {
  color: #16cc80;
}
/*轮播图内容*/
.cont {
  width: 80%;
  margin-left: 20%;
  height: 1600rpx;
  padding-top: 25rpx;
  font-size: 28rpx;
}
.cont .date {
  text-align: center;
}
.cont swiper-item {
  width: auto;
  height: 100%;
  /* background-color: #5fd9a6; */
  border: 1rpx solid #ebebeb;
  font-size: 35rpx;
  box-sizing: border-box;
}
.todays {
  height: 200rpx;
}
p {
  height: 80rpx;
  line-height: 80rpx;
  color: cornflowerblue;
  font-size: 42rpx;
  text-align: center;
}
.date {
  height: 80rpx;
  line-height: 80rpx;
  margin-top: 10rpx;
  text-align: center;
}
.sum {
  height: 180rpx;
  margin-top: 10rpx;
}
.Qc {
  display: flex;
  justify-content: space-around;
  margin-top: 10rpx;
}
.zhi {
  margin-top: 10rpx;
  height: 240rpx;
}
.zhi b {
  color: darkgoldenrod;
}
.zhi span {
  display: inline-block;
  width: 80%;
  height: 80rpx;
  line-height: 80rpx;
}
</style>
 
