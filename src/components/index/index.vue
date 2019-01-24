<template>
  <!-- 用户管理 -->
  <div>
    <div class="header">
      <div class="jd">JD-SHOP</div>
      <div class="title">
        <span class="tit">后台管理系统</span>
        <span class="user">当前用户：admin</span>
      </div>
    </div>

    <el-container>
      <!-- 导航条 -->
      <el-aside width="17vw">
        <el-menu
          default-active="1"
          class="el-menu-vertical-demo"
          style="height:90vh;"
          @select="handleSelect"
        >
          <el-menu-item index="1">
            <span slot="title">用户管理</span>
          </el-menu-item>
          <el-menu-item index="2">
            <span slot="title">订单管理</span>
          </el-menu-item>
          <el-menu-item index="3">
            <span slot="title">商品管理</span>
          </el-menu-item>
          <el-menu-item index="4">
            <span slot="title">修改资料</span>
          </el-menu-item>
        </el-menu>
      </el-aside>

      <!-- 用户管理 -->
      <el-main class="main" v-show="user">
        <div class="title">用户管理</div>
        <el-table
          :data="userData"
          border
          style="width: 100%"
          :header-cell-style="{'font-weight':700}"
        >
          <el-table-column prop="id" label="_id" width="270" header-align="center" align="center"></el-table-column>
          <el-table-column prop="name" label="用户名" width="220" header-align="center" align="center"></el-table-column>
          <el-table-column
            prop="telNum"
            label="手机号码"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column
            prop="password"
            label="密码"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column label="操作" header-align="center" align="center">
            <template slot-scope="scope">
              <el-button size="mini">编辑</el-button>
              <el-button size="mini" type="danger">删除</el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-main>

      <!-- 订单管理 -->
      <el-main class="main" v-show="order">
        <div class="title">订单管理</div>
        <el-table :data="orderData" border style="width: 100%">
          <el-table-column
            fixed
            prop="id"
            label="_id"
            width="270"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column
            prop="orderNum"
            label="订单号"
            width="160"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column prop="name" label="收货人" width="220" header-align="center" align="center"></el-table-column>
          <el-table-column
            prop="telNum"
            label="联系电话"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column
            prop="address"
            label="收货地址"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column
            prop="price"
            label="订单总价"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column label="操作" header-align="center" align="center">
            <template slot-scope="scope">
              <el-button size="mini">编辑</el-button>
              <el-button size="mini" type="danger">删除</el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: true,
      order: false,
      userData: [
        {
          id: "5bd99a8aa655750dd4879b81",
          name: "小仙女是我",
          telNum: "15214647650",
          password: "123"
        },
        {
          id: "5bd99a8aa655750dd4879b81",
          name: "小仙女是我",
          telNum: "15214647650",
          password: "123"
        }
      ],
      orderData: [
        {
          id: "5bd99a8aa655750dd4879b81",
          orderNum: "1547006475008",
          name: "鹏鹏",
          telNum: "15214647650",
          address: "黑龙江省哈尔滨市香坊区东北农业大学",
          price: "35.90"
        }
      ]
    };
  },
  methods: {
    handleSelect(index, indexPath) {
      if (index == 1) {
        this.user = true;
        this.order = false;
      }
      if (index == 2) {
        this.user = false;
        this.order = true;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
