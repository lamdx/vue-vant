<template>
  <div class="goodinfo">
    <navbar title="商品详情"></navbar>
    <!-- 轮播图 -->
    <swiper :bannerlist="bannerlist" :isfull="true"></swiper>
    <v-touch v-on:swiperight="onSwipeRight" tag="div">
      <!-- 价格 -->
      <van-cell value="已售1.1万" value-class="price">
        <template slot="title">
          <span class="custom-title price">￥129-298</span>
        </template>
      </van-cell>
      <!-- 商品保障 -->
      <van-cell>
        <van-row>
          <van-col span="6">
            <van-icon name="success" color="#f00" />正品保障
          </van-col>
          <van-col span="6">
            <van-icon name="success" color="#f00" />假一赔十
          </van-col>
          <van-col span="6">
            <van-icon name="success" color="#f00" />权威检测
          </van-col>
          <van-col span="6">
            <van-icon name="success" color="#f00" />无忧退货
          </van-col>
        </van-row>
      </van-cell>
      <van-cell value="" is-link>
        <template slot="title">
          <van-tag type="danger" size="large" round>满额减</van-tag>
          <span class="custom-title">满200减20</span>
        </template>
      </van-cell>
      <van-cell value="下单自动改价" is-link>
        <!-- 使用 title 插槽来自定义标题 -->
        <template slot="title">
          <span class="custom-title">APP购买立省</span>
          <van-tag type="danger">6元</van-tag>
        </template>
      </van-cell>
      <!-- 选择规格数量 -->
      <van-cell value="" is-link @click="show = !show">
        <template slot="title">
          <span>{{ desc }}</span>
        </template>
      </van-cell>
      <van-cell value="该商品支持全国配送" is-link>
        <template slot="title">
          <span class="custom-title">发货</span>
        </template>
      </van-cell>
      <van-panel title="CEMOY肌XXXXXXXXXXXXXX">
        <div slot="footer">
          使用babel-plugin-import插件，它是一款babel插件，它能够在编译的过程中将import的写法自动转换为按需求引入的方式，使用babel-plugin-import插件，它是一款babel插件，它能够在编译的过程中将import的写法自动转换为按需求引入的方式
        </div>
      </van-panel>
      <!-- 图片详情 -->
      <van-image
        fit="contain"
        src="//img30.360buyimg.com/sku/jfs/t1/44049/29/7647/169103/5d131215Eeec170f9/aefd36177979a718.jpg"
        v-for="item in 3"
        :key="item"
      />
      <!-- 底部 -->
      <van-goods-action>
        <van-goods-action-icon icon="service-o" text="客服" />
        <van-goods-action-icon
          icon="shop-o"
          text="商城"
          to="/cart"
        />
        <van-goods-action-icon
          icon="shopping-cart-o"
          text="购物车"
          :info="getAllCount"
          to="/cart"
        />
        <van-goods-action-button
          type="warning"
          text="加入购物车"
          @click="addSubmit"
        />
        <van-goods-action-button type="danger" text="立即购买" />
      </van-goods-action>
      <!-- 底部弹框 -->
      <van-popup
        v-model="show"
        round
        closeable
        position="bottom"
        :style="{ height: '40%' }"
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
    </v-touch>
  </div>
</template>
<script>
import navbar from "../../components/Navbar";
import swiper from "../../components/Swiper";
import { mapActions, mapGetters } from "vuex";
import { Toast } from "vant";
export default {
  data() {
    return {
      bannerlist: [
        {
          id: 1,
          tilte: "首页轮播图商品1",
          imgsrc:
            "https://img20.360buyimg.com/babel/s590x470_jfs/t1/101512/38/7437/86371/5dfb8719E05c324e5/0b2ec8eb3e2fc480.jpg.webp",
          href: "/search"
        },
        {
          id: 2,
          tilte: "首页轮播图商品2",
          imgsrc:
            "https://img20.360buyimg.com/babel/s590x470_jfs/t1/101512/38/7437/86371/5dfb8719E05c324e5/0b2ec8eb3e2fc480.jpg.webp",
          href: "/cart"
        },
        {
          id: 3,
          tilte: "首页轮播图商品3",
          imgsrc:
            "https://img20.360buyimg.com/babel/s590x470_jfs/t1/101512/38/7437/86371/5dfb8719E05c324e5/0b2ec8eb3e2fc480.jpg.webp",
          href: "/member"
        },
        {
          id: 4,
          tilte: "首页轮播图商品4",
          imgsrc:
            "https://img20.360buyimg.com/babel/s590x470_jfs/t1/101512/38/7437/86371/5dfb8719E05c324e5/0b2ec8eb3e2fc480.jpg.webp",
          href: "/cart"
        }
      ],
      show: false, // 弹框
      num: 1, // 购买数量
      flag: "", // 选中的规格
      pic: "",
      price: "",
      desc: "请选择规格属性",
      specs: [
        // 规格
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
      ],
      canclick: true, // 防抖开关
      goodsinfo: {
        id: 1,
        uid: 1,
        productId: 1,
        num: 1, // 购买数量
        size: 42,
        isDelete: 0,
        isSelected: 1,
        price: 6999,
        desc:
          "酷睿双核i5处理器|256GB SSD|8GB内存|英特尔HD显卡620含共享显卡内存",
        title: "Apple MacBook Air系列",
        thumb: "/img/index/study_computer_img1.png"
      },
      goodsinfo2: {
        id: 2,
        uid: 1,
        productId: 2,
        num: 2, // 购买数量
        size: 42,
        isDelete: 0,
        isSelected: 1,
        price: 3899,
        desc: "酷睿双核i5处理器|512GB SSD|2GB内存|英特尔HD独立显卡",
        title: "小米Air 金属超轻薄",
        thumb: "/img/index/study_computer_img2.png"
      },
      goodsinfo3: {
        id: 3,
        uid: 1,
        productId: 3,
        num: 1, // 购买数量
        size: 42,
        isDelete: 0,
        isSelected: 1,
        price: 99,
        desc:
          "华硕(ASUS)13.3英寸RX310UQ金属超极本 学生 商务手提轻薄便携超薄笔记本电脑 玫瑰金 13.3英寸I3-7100U/4G/128G固态",
        title: "华硕RX310 金属超极本",
        thumb: "/img/index/study_computer_img3.png"
      },
      goodsinfo4: {
        id: 4,
        uid: 1,
        productId: 4,
        num: 1, // 购买数量
        size: 42,
        isDelete: 0,
        isSelected: 1,
        price: 399,
        desc:
          "华硕(ASUS)13.3英寸RX310UQ金属超极本 学生 商务手提轻薄便携超薄笔记本电脑 玫瑰金 13.3英寸I3-7100U/4G/128G固态",
        title: "华硕RX310 金属超极本",
        thumb: "/img/index/study_computer_img1.png"
      }
    };
  },
  created() {
    this.hande(this.ins);
    if (window.localStorage.getItem("token")) {
      this.getCart();
    }
  },
  methods: {
     ...mapActions(["postCart"]),
    // 选择商品规格
    select(id, name, pic, price) {
      this.flag = id;
      this.desc = "已选择：" + name;
      this.pic = pic;
      this.price = price;
    },
    add(goodsInfo) {
      if (this.canclick) {
        this.canclick = false;
        setTimeout(() => {
          this.postCart(goodsInfo);
          this.canclick = true;
        }, 300);
      }
    },
    //获取添加商品信息
    onClickButtonSubmit() {
      if (this.price == "") {
        console.log("请选择规格");
        this.$notify({
          message: "请选择规格",
          color: "#ad0000",
          background: "#ffe1e1"
        });
      } else {
        let params = {
          // price:this.price,
          // addshop:this.addshop
          gid: this.gid, //  商品gid
          name: this.name, //  商品名字
          number: this.number, //  购买数量
          price: this.price, //    售价
          desc_title: this.desc_title, // 商品标题
          describ: this.describ, //  描述商品信息
          sorts: this.sorts, //  种类
          img_url: this.img_url //  图片途径
        };
        // this.$minApi.addCar(params).then(res=>{
        // })
        console.log(params);
        this.show = !this.show;
        this.$toast({
          message: "添加成功",
          icon: "success",
          duration: 300
        });
      }
    },
    // 加入购物车
    addSubmit() {
      if (this.price == "") {
        //判断用户有没有选择规格
        this.show = !this.show;
      } else {
        //将商品添加到购物车
        let params = {
          id: this.gid,
          uid: 1,
          gid: this.gid,
          number: this.number,
          name: this.name,
          status: 1,
          isChecked: 1,
          price: this.price,
          describ: this.describ,
          desc_title: this.desc_title,
          img_url: this.img_url
        };
        if (this.canclick) {
          this.canclick = false;
          setTimeout(() => {
            if (window.localStorage.getItem("token")) {
              this.postCart(params);
              this.$toast({
                message: "添加成功",
                icon: "success",
                duration: 500
              });
            } else {
              this.$router.push({
                path: `/login/login?redirect=${this.$route.path}`
              });
            }
            this.canclick = true;
          }, 300);
        }
      }
    },
    onSwipeRight() {
      //  console.log("右滑")
      this.$router.go(-1);
    }
  },
  computed: {
    ...mapGetters(["getAllCount"])
  },
  components: {
    navbar,
    swiper
  }
};
</script>
<style lang="scss" scoped>
.goodinfo {
  padding-top: 45px;
  .price {
    color: #f00;
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
