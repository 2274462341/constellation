<template>
  <div class="todays">
    <p class="ps">{{todayArr.name}}</p>
    <div class="date">{{todayArr.datetime}}</div>
    <div class="Qc">
      <p>
        <b>速配星座：</b>
        <span>{{todayArr.QFriend}}</span>
      </p>
      <p>
        <b>幸运色：</b>
        <span>{{todayArr.color}}</span>
      </p>
      <p>
        <b>幸运数字：</b>
        <span>{{todayArr.number}}</span>
      </p>
      <p>
        <b>综合指数：</b>
        <span>{{todayArr.all}}</span>
      </p>
      <p>
        <b>爱情指数：</b>
        <span>{{todayArr.love}}</span>
      </p>
      <p>
        <b>财运指数：</b>
        <span>{{todayArr.money}}</span>
      </p>
      <p>
        <b>健康指数：</b>
        <span>{{todayArr.health}}</span>
      </p>
      <p>
        <b>事业指数：</b>
        <span>{{todayArr.work}}</span>
      </p>
    </div>
    <div class="sum">{{todayArr.summary}}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      val: "",
      todayArr: {},
      img: ""
    };
  },
  onLoad(options) {
    console.log(options.name);
    this.val = options.name;
    wx.request({
      url:
        "http://web.juhe.cn:8080/constellation/getAll?key=f0c93a2f51f2a010953f9b947bf130ca",
      header: { "content-type": "application/json" },
      data: {
        consName: this.val
      },
      success: result => {
        this.todayArr = result.data.today;
      }
    });
  }
};
</script>
<style>
.todays {
  width: 100%;
  height: 1500rpx;
  background: #6e82ee;
}

.ps {
  height: 80rpx;
  line-height: 80rpx;
  text-align: center;
  font-size: 50rpx;
  color: blueviolet;
}

.date {
  height: 80rpx;
  line-height: 80rpx;
  text-align: center;
  font-size: 38rpx;
}
.Qc {
  height: 500rpx;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  margin-top: 50rpx;
}
.Qc p {
  width: 30%;
  height: 100rpx;
  display: flex;
  flex-direction: column;
}
.sum {
  width: 80%;
  border: solid 3px #ccc;
  border-radius: 20px;
  height: 260rpx;
  margin-left: 10%;
}
</style>
