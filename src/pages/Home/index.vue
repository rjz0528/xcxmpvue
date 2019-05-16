<template>
  <!--结构-->
  <!--template 标签是h5 标签 特点只执行 不在浏览器显示全部代码结构要求之一个唯一的根节点《< div p  等等都可以-->
  <div>
    <!-- // ? 搜索 -->
    <div class="chars">
      <div class="search">
        <icon class="searchs" type="search"></icon>
        <span>搜索</span>
      </div>
    </div>
    <!-- // ?轮播图 -->
    <swiper
    indicator-dots 
    indicator-active-color="#FFFFF0"
    :autoplay="true"
    circular
    :interval="intervaltime">
        <swiper-item v-for="item in imgUrls" :key="item.goods_id">
          <image :src="item.image_src" class="slide-image" width="355" height="150"/>
        </swiper-item>
    </swiper>
  </div>
</template>

<script>
//行为
export default {
  // ?生命周期函数
  created() {
    this.swiptdata()
  },
  data () {
    return {
      imgUrls: [],
      // ?轮播图切换的时间长度
      intervaltime:3000
    };
  },
  methods: {
    swiptdata() {
      mpvue.request({
        url:'https://www.zhengzhicheng.cn/api/public/v1/home/swiperdata',
        success: (res) =>{
          // console.log(res.data)
          if(res.data.meta.status !== 200) {
            return console.log('获取错误')
          }
          console.log(res.data.message)
          this.imgUrls = res.data.message
        }
      })
    }
  }
};
</script>

<style  scoped>
/*样式*/
.chars {
  background-color: #eb4450;
  padding: 20rpx;
}

.search {
  /* margin: 30rpx 20rpx 0  20rpx; */
  height: auto;
  text-align: center;
  background-color: #fff;
  /* text-align: center; */
}
.searchs {
  /* vertical-align:middle */
  vertical-align: middle;
}
.slide-image{
  width: 750rpx;
  height: 100%;
}
</style>
