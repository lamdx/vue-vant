<template>
  <div class="member">
    <div class="header">
      <!-- 设置 -->
      <p class="settings">
        <router-link to="/member/settings"
          ><van-icon name="setting-o" size="20"
        /></router-link>
        <router-link to="/member/settings"
          ><van-icon name="chat-o" size="20"
        /></router-link>
      </p>
      <!-- 头像信息 -->
      <van-row justify="center">
        <van-col span="4" offset="1">
          <van-image
            round
            width="50"
            height="50"
            lazy-load
            src="/img/index/avatar-default.png"
          />
        </van-col>
        <van-col span="8">
          <p>{{ uname }}</p>
        </van-col>
      </van-row>
    </div>
    <!-- 订单/购物车/优惠券/收藏 -->
    <div class="content">
      <ul>
        <li>
          <router-link to="/cart">
            <van-icon name="orders-o" size="30" color="#f94a44" />
            <p>订单</p>
          </router-link>
        </li>
        <li>
          <router-link to="/cart">
            <van-icon name="shopping-cart-o" size="30" color="#f94a44" />
            <p>购物车</p>
          </router-link>
        </li>
        <li>
          <router-link to="/cart">
            <van-icon name="coupon-o" size="30" color="#f94a44" />
            <p>优惠券</p>
          </router-link>
        </li>
        <li>
          <router-link to="/cart">
            <van-icon name="star-o" size="30" color="#f94a44" />
            <p>我的收藏</p>
          </router-link>
        </li>
      </ul>
    </div>
    <van-panel title="我的订单" status="查看全部订单>" @click="viewOrder">
      <div class="order">
        <ul>
          <li>
            <router-link to="/cart">
              <van-icon name="orders-o" size="30" color="#f94a44" />
              <p>待付款</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="shopping-cart-o" size="30" color="#f94a44" />
              <p>待发货</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="coupon-o" size="30" color="#f94a44" />
              <p>待收货</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="star-o" size="30" color="#f94a44" />
              <p>评价</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="star-o" size="30" color="#f94a44" />
              <p>退款/售后</p>
            </router-link>
          </li>
        </ul>
      </div>
    </van-panel>
    <van-panel title="必备工具" status="查看全部工具>" @click="viewTool">
      <div class="order">
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
      </div>
    </van-panel>
    <van-panel title="我关注的频道" status="去关注更多>" @click="viewOrder">
      <div class="channel">
        <ul>
          <li>
            <router-link to="/cart">
              <van-icon name="orders-o" size="30" color="#f94a44" />
              <p>待付款</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="shopping-cart-o" size="30" color="#f94a44" />
              <p>待发货</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="coupon-o" size="30" color="#f94a44" />
              <p>待收货</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="star-o" size="30" color="#f94a44" />
              <p>评价</p>
            </router-link>
          </li>
          <li>
            <router-link to="/cart">
              <van-icon name="star-o" size="30" color="#f94a44" />
              <p>退款/售后</p>
            </router-link>
          </li>
        </ul>
      </div>
    </van-panel>
  </div>
</template>
<script>
import { mapState } from "vuex";
export default {
  methods: {
    viewOrder() {},
    viewTool() {}
  },
  computed: {
    ...mapState(["uname"])
  }
};
</script>
<style lang="scss" scoped>
.member {
  .header {
    padding-bottom: 20px;
    background-size: 60px 60px;
    background-image: linear-gradient(
      -45deg,
      #f83e37 0%,
      #f83e37 25%,
      #ef3630 25%,
      #ef3630 50%,
      #f83e37 50%,
      #f83e37 75%,
      #ef3630 75%,
      #ef3630 100%
    );
  }
  .settings {
    margin: 0;
    padding: 10px;
    text-align: right;
  }
  .content,
  .order,
  .channel {
    padding: 5px;
    margin-bottom: 10px;
    border: 1px solid #fff;
    // border-radius: 15px;
    background: #fff;
    color: #000;
    ul {
      display: flex;
      text-align: center;
      li {
        flex-grow: 1;
        p {
          color: #000;
        }
      }
    }
  }
  .van-panel__header-value {
    color: #666;
    font-weight: normal;
  }
  .van-cell {
    font-weight: bold;
  }
}
</style>
