<template>
  <div class="home">
    <!-- 搜索栏 -->
    <form action="/">
      <van-search
        v-model="value"
        shape="round"
        background="#f83e37"
        placeholder="请输入搜索关键词"
        @search="onSearch"
        @cancel="onCancel"
      />
    </form>
    <!-- 轮播图 swiper -->
    <swiper :bannerlist="bannerlist" :isfull="true"></swiper>
    <!-- grid 宫格 -->
    <van-grid :border="false" :column-num="3">
      <van-grid-item to="/search">
        <van-image
          round
          width="3rem"
          height="3rem"
          src="/img/index/menu1.png"
        />
        <span>新闻资讯</span>
      </van-grid-item>
      <van-grid-item to="/search">
        <van-image
          round
          width="3rem"
          height="3rem"
          src="/img/index/menu2.png"
        />
        <span>图片分享</span>
      </van-grid-item>
      <van-grid-item>
        <van-image
          round
          width="3rem"
          height="3rem"
          src="/img/index/menu3.png"
        />
        <span>商品购买</span>
      </van-grid-item>
      <van-grid-item>
        <van-image
          round
          width="3rem"
          height="3rem"
          src="/img/index/menu4.png"
        />
        <span>视频专区</span>
      </van-grid-item>
      <van-grid-item>
        <van-image
          round
          width="3rem"
          height="3rem"
          src="/img/index/menu5.png"
        />
        <span>留言反馈</span>
      </van-grid-item>
      <van-grid-item>
        <van-image
          round
          width="3rem"
          height="3rem"
          src="/img/index/menu6.png"
        />
        <span>联系我们</span>
      </van-grid-item>
    </van-grid>
    <!-- 每日推荐 -->
    <div class="recommend">
      <h3 class="title">每日推荐</h3>
      <van-row>
        <van-col
          span="12"
          v-for="(item, index) in goods"
          :key="index"
          @click.stop="view(index)"
        >
          <div class="part">
            <span class="tag">商品直供</span>
            <img :src="item.pic" alt="" v-lazy="item.pic" />
            <p class="p1">{{ item.title }}</p>
            <p class="p2">{{ item.discount }}</p>
            <div class="footer">
              <span> ￥{{ item.price }} </span>
              <div class="icon">
                <van-icon
                  @click.stop="addcart(item.id)"
                  color="red"
                  size="20px"
                  name="cart-o"
                />
              </div>
            </div>
          </div>
        </van-col>
      </van-row>
    </div>
    <!-- 底部弹框 -->
    <van-popup
      v-model="show"
      round
      closeable
      position="bottom"
      :style="{ height: '50%' }"
    >
      <div class="title">
        <img :src="pic" alt="" />
        <div class="right">
          <p>￥{{ price }}</p>
          <span>{{ desc }}</span>
        </div>
      </div>
      <p class="size">规格</p>
      <div class="section">
        <span
          v-for="(item, index) in specs"
          :key="index"
          :class="{ active: item.id == flag }"
          @click="select(item.id, item.name, item.pic, item.price)"
        >
          {{ item.name }}
        </span>
      </div>
      <p class="number">
        <span>购买数量</span>
        <van-stepper v-model="num" />
      </p>
      <van-goods-action class="submit">
        <van-goods-action-button
          size="large"
          type="warning"
          text="加入购物车"
        />
        <van-goods-action-button size="large" type="danger" text="立即购买" />
      </van-goods-action>
    </van-popup>
  </div>
</template>
<script>
import { getBanner } from "../../assets/api/home.js";
//      对象解构        模块对象，其中包含 getIndex()
import swiper from "../../components/Swiper";
import { Toast } from "vant";
export default {
  data() {
    return {
      value: "", // 搜索值
      bannerlist: [{ imgsrc: "" }], // 轮播图
      goods: [
        {
          pic:
            "https://img14.360buyimg.com/babel/s590x470_jfs/t1/88653/22/5614/83757/5dee0bffE4ab62eac/ba3fc193c0aba7f0.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "1"
        },
        {
          pic:
            "https://img13.360buyimg.com/pop/s590x470_jfs/t1/91012/29/6857/44545/5df728ccE01cae02f/3f7353e56af4c21c.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "2"
        },
        {
          pic:
            "https://img10.360buyimg.com/pop/s590x470_jfs/t1/47443/16/16570/74911/5ddc9264Ea6842152/dd62c697b91a393d.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "3"
        },
        {
          pic:
            "https://img11.360buyimg.com/pop/s590x470_jfs/t1/106330/4/2361/91530/5dcfb10dEe4f5a13b/0c27620b96ea6e3f.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "4"
        },
        {
          pic:
            "https://img13.360buyimg.com/pop/s590x470_jfs/t1/89794/4/7076/70841/5df7638eE060a8256/d84cbef36453a542.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "5"
        },
        {
          pic:
            "https://img30.360buyimg.com/pop/s590x470_jfs/t1/87876/24/5915/54155/5df04cc4Eddd41069/3f69d04f2766b358.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "6"
        },
        {
          pic:
            "https://img11.360buyimg.com/jdcms/s150x150_jfs/t1/88872/34/7366/168722/5dfaf90dE8aad757f/2d21a8f7ebe86f57.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*25 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "300",
          id: "7"
        },
        {
          pic:
            "https://img10.360buyimg.com/jdcms/s150x150_jfs/t1/74281/23/15407/185540/5dceca44E41c54c44/4197eaeeac500a51.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "248",
          id: "8"
        },
        {
          pic:
            "https://img13.360buyimg.com/jdcms/s150x150_jfs/t1/73585/10/8927/211662/5d6e7bb7Ec6b089d5/b28c98d79261873e.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "9"
        },
        {
          pic:
            "https://img20.360buyimg.com/jdcms/s150x150_jfs/t1/80225/26/591/103895/5ceced2eEc6af47cd/c282b43454ede3db.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "10"
        },
        {
          pic:
            "https://img13.360buyimg.com/jdcms/s150x150_jfs/t1/21942/11/7639/117978/5c6e5999E6f04f9b5/6e096590c298e44c.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "11"
        },
        {
          pic:
            "https://img20.360buyimg.com/jdcms/s150x150_jfs/t1252/241/1006632532/219845/2c11e4d6/55688cb4N939c7429.jpg.webp",
          title: "蒙牛 低脂高钙牛奶 250ml*24 礼盒装",
          discount:
            "【部分2件9折】暖心牛奶，陪你过冬，部分爆款低至2件9折抢购，戳此查看快来",
          price: "218",
          id: "12"
        }
      ],
      show: false, // 弹框
      num: 1, // 购买数量
      flag: "", // 选择规格
      pic: "",
      price: "",
      desc: "请选择规格属性",
      specs: [
        {
          id: 1,
          name: "水120ml",
          pic:
            "//img30.360buyimg.com/sku/jfs/t1/88678/2/8001/535168/5e0076faE562152e5/59df511be198196d.jpg",
          price: "50"
        },
        {
          id: 2,
          name: "水140ml",
          pic:
            "//m.360buyimg.com/mobilecms/s750x750_jfs/t1/31624/11/14623/110411/5cbee9a3E956ab4c4/bd040c6a29865ed7.jpg!q80.dpg.webp",
          price: "480"
        },
        {
          id: 3,
          name: "水180ml",
          pic:
            "//img.alicdn.com/imgextra/i3/3406142004/O1CN01iFTMQI1QfsIGn60x5_!!3406142004.jpg_640x640q80_.webp",
          price: "444"
        }
      ]
    };
  },
  created() {
    getBanner().then(res => (this.bannerlist = res));
  },
  methods: {
    // 搜索
    onSearch(val) {
      Toast(val);
    },
    onCancel() {
      Toast("取消");
    },
    // 加入购物车
    addcart(id) {
      console.log("商品id", id);
      this.show = !this.show;
    },
    // 选择商品规格
    select(id, name, pic, price) {
      this.flag = id;
      this.desc = "已选择：" + name;
      this.pic = pic;
      this.price = price;
    },
    // 查看商品详情 跳转页还没有完成
    view(id) {
      console.log("进入详情id", id);
      this.$router.push({ path: `/mysearch/goodlist/${id}` });
    }
  },
  components: {
    swiper
  }
};
</script>
<style lang="scss">
.home {
  .van-grid-item__content {
    span {
      font-size: 0.8rem;
    }
  }
  .recommend {
    .title {
      height: 75px;
      line-height: 75px;
      margin: 5px 0;
      text-align: center;
      color: #ff3600;
      background-color: #fff;
    }
    .part {
      background-color: #fff;
      box-shadow: 0 1px 2px rgba(10, 16, 20, 0.24);
      border-radius: 5px;
      padding: 10px;
      margin: 5px;
      .tag {
        padding: 0 5px;
        border: 1px red solid;
        border-radius: 20px;
        font-size: 0.75rem;
        color: red;
      }
      img {
        width: 100%;
      }
      p {
        margin: 0;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
      .p1 {
        font-weight: 600;
      }
      .p2 {
        padding-top: 6px;
        font-size: 0.8rem;
        color: #666;
      }
      .footer {
        display: flex;
        justify-content: space-between;
        padding-top: 10px;
        span {
          font-weight: 600;
          color: red;
        }
        .icon {
          i {
            width: 25px;
            height: 25px;
            line-height: 25px;
            border: 1px red solid;
            border-radius: 25px;
            text-align: center;
          }
        }
      }
    }
  }
  .van-popup {
    overflow-y: inherit;
    .title {
      display: flex;
      border-bottom: 1px solid #f3f3f3;
      height: 120px;
      img {
        width: 125px;
        height: 125px;
        position: relative;
        left: 20px;
        top: -20px;
        border-radius: 8px;
      }
      .right {
        padding-left: 30px;
        p {
          color: red;
        }
      }
    }
    .size {
      padding-left: 10px;
      font-size: 14px;
    }
    .section {
      display: flex;
      height: 50px;
      border-bottom: 1px solid #f3f3f3;
      span {
        width: 80px;
        height: 30px;
        line-height: 30px;
        margin: 0 5px;
        border-radius: 20px;
        background-color: #f7f7f7;
        font-size: 0.75rem;
        text-align: center;
      }
      .active {
        background-color: #fa4930;
        color: #f7f7f7;
      }
    }
    .number {
      display: flex;
      justify-content: space-between;
      padding: 0 10px;
    }
  }
}
</style>
