<template>

  <div class="layout" v-if="completed">
    <Layout>
      <Header>
        <Menu mode="horizontal" theme="dark" active-name="1">
          <div class="layout-logo">
            <span class="inner-text">管理平台</span>
          </div>
          <div class="layout-nav">
            <MenuItem name="1" to="/app/stance">
            <Icon type="ios-navigate"></Icon>
            内容管理
            </MenuItem>
            <MenuItem name="2" to="/app/system">
            <Icon type="ios-analytics"></Icon>
            系统管理
            </MenuItem>
          </div>
        </Menu>
      </Header>
      <Content>
        <router-view></router-view>
      </Content>
      <Footer>Footer</Footer>
    </Layout>
  </div>
</template>

<script>
export default {
  name: "index",
  data() {
    return {
      completed: false
    };
  },
  mounted() {
    if (sessionStorage.getItem("UserName")) {
      this.completed = true;
    } else {
      this.completed = false;
      this.$Modal.error({
        title: "错误信息",
        content: "您的用户状态已失效，请前往登录页面重新登录",
        onOk: () => {
          this.$router.replace("/login");
        }
      });
    }
  },
  methods: {}
};
</script>

<style scoped lang="scss" rel="stylesheet/scss">
.layout {
  position: relative;
  min-width: 1100px;
  background: #f5f7f9;

  > .ivu-layout {
    display: flex;
    flex: auto;
    flex-direction: column;
    background: #f5f7f9;
    > .ivu-layout-header {
      > .ivu-menu {
        display: flex;

        height: 64px;
        line-height: 64px;
        > .layout-logo {
          display: inline-block;
          height: 64px;
          vertical-align: middle;

          > .inner-text {
            display: inline-block;
            margin: 20px 0 20px 10px;
            padding: 0 5px;
            background-color: rgba(0, 0, 0, 0.2);
            color: #fff;
            line-height: 22px;
            height: 22px;
            border-radius: 2px;
            vertical-align: middle;
          }
        }
        > .layout-nav {
          width: 240px;
        }
      }
    }
  }

  .layout-footer-center {
    text-align: center;
  }
}
</style>
