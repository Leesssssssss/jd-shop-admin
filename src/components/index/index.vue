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
          style="width: 100%"
          :header-cell-style="{'font-weight':700}"
        >
          <el-table-column prop="_id" label="_id" width="270" header-align="center" align="center"></el-table-column>
          <el-table-column
            prop="userName"
            label="用户名"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
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
        <el-table :data="orderData" style="width: 100%">
          <el-table-column type="expand">
            <template slot-scope="props">
              <el-form label-position="left" inline class="table-expand">
                <el-form-item label="订单 ID">
                  <span>{{ props.row._id }}</span>
                </el-form-item>
                <el-form-item label="订单号">
                  <span>{{ props.row.orderNum }}</span>
                </el-form-item>
                <el-form-item label="收货人">
                  <span>{{ props.row.address.name }}</span>
                </el-form-item>
                <el-form-item label="电话号码">
                  <span>{{ props.row.address.telNum }}</span>
                </el-form-item>
                <el-form-item label="收货地址">
                  <span>{{ props.row.address.city + props.row.address.addressDetail }}</span>
                </el-form-item>
                <el-form-item label="订单总价">
                  <span>{{ props.row.price }}</span>
                </el-form-item>
                <div v-for="good in props.row.goods">
                  <el-form-item label="商品名称">
                    <span>{{ good.goodName }}</span>
                  </el-form-item>
                  <el-form-item label="商品数量">
                    <span>{{ good.count }}</span>
                  </el-form-item>
                  <el-form-item label="商品单价">
                    <span>{{ good.price }}</span>
                  </el-form-item>
                </div>
              </el-form>
            </template>
          </el-table-column>
          <el-table-column label="订单 ID" prop="_id"></el-table-column>
          <el-table-column label="订单号" prop="orderNum"></el-table-column>
          <el-table-column label="收货人" prop="address.name"></el-table-column>
          <el-table-column label="电话号码" prop="address.telNum"></el-table-column>
          <el-table-column label="操作" header-align="center" align="center">
            <template slot-scope="scope">
              <el-button size="mini">编辑</el-button>
              <el-button size="mini" type="danger">删除</el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-main>

      <!-- 商品管理 -->
      <el-main class="main" v-show="good">
        <div class="title">商品管理</div>
        <el-table
          :data="goodData"
          style="width: 100%"
          :header-cell-style="{'font-weight':700}"
        >
          <el-table-column prop="_id" label="_id" width="270" header-align="center" align="center"></el-table-column>
          <el-table-column
            prop="userName"
            label="商品名称"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column
            prop="telNum"
            label="商品单价"
            width="220"
            header-align="center"
            align="center"
          ></el-table-column>
          <el-table-column
            prop="password"
            label="商品分类"
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
import axios from "axios";
export default {
  data() {
    return {
      user: true,
      order: false,
      good: false,
      userData: [],
      orderData: [],
      goodData: []
    };
  },
  created() {
    axios.get("http://localhost:7001/getUserInfo").then(res => {
      console.log(res);
      this.userData = res.data;
      for (var i = 0; i < res.data.length; i++) {
        this.orderData = this.orderData.concat(res.data[i].order);
      }
    });
  },
  methods: {
    handleSelect(index, indexPath) {
      if (index == 1) {
        this.user = true;
        this.order = false;
        this.good = false;
      }
      if (index == 2) {
        this.user = false;
        this.order = true;
        this.good = false;
      }
      if (index == 3) {
        this.user = false;
        this.order = false;
        this.good = true;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
