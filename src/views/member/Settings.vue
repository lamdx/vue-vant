<template>
  <div class="member">
    <van-nav-bar title="设置" fixed>
      <van-icon name="arrow-left" slot="left" @click="goBack" />
    </van-nav-bar>
    <div class="header">
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
    <van-cell-group>
      <van-cell
        title="收货地址管理"
        icon="location-o"
        size="large"
        is-link
        to="/member/address"
      >
      </van-cell>
      <van-cell
        title="账号与安全"
        icon="user-o"
        size="large"
        is-link
        to="/member/account"
      >
      </van-cell>
      <van-cell
        title="隐私"
        icon="user-o"
        size="large"
        is-link
        to="/member/account"
      >
      </van-cell>
      <van-cell
        title="通用"
        icon="user-o"
        size="large"
        is-link
        to="/member/account"
      >
       </van-cell>
      <van-cell
        title="问题反馈"
        icon="user-o"
        size="large"
        is-link
        to="/member/account"
      >
      </van-cell>
    </van-cell-group>
    <van-divider></van-divider>
    <van-button size="large" @click="logout">
      切换账号
    </van-button>
    <van-divider></van-divider>
    <van-button size="large" @click="logout">
      退出登录
    </van-button>
  </div>
</template>
<script>
import { mapState } from "vuex";
export default {
  methods: {
    logout() {
      window.localStorage.removeItem("token");
      this.$store.state.cart = [];
      this.$router.push({ path: `/home` });
    },
    // 点击后退
    goBack() {
      this.$router.go(-1);
    }
  },
  computed: {
    ...mapState(["uname"])
  }
};
</script>
<style lang="scss" scoped>
.member {
  padding-top: 45px;
  .header{
    padding: 15px;
    background-color: #fff;
  }
}
</style>
