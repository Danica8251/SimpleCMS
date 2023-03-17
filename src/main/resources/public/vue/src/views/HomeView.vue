<template>
    <el-container style="min-height: 100vh">
      <!--   側邊欄 開始   -->
      <el-aside :width="sideWidth + 'px'" style="background-color: rgb(238, 241, 246);">
        <el-menu :default-openeds="['1', '3']" style="min-height: 100%; overflow-x: hidden"
                 background-color="rgb(48, 65, 86)"
                 text-color="#fff"
                 active-text-color="#ffd04b"
                 :collapse-transition="false"
                 :collapse="isCollpase"
        >
          <div style="height: 60px; line-height: 60px; text-align: center">
            <img src="../assets/logo.png" alt="" style="width: 20px; position: relative; top: 5px; margin-right: 5px">
            <b style="color: white" v-show="logoTextShow">後台管理系統</b>
          </div>
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-message"></i>
              <span slot="title">導航一</span>
            </template>
            <el-menu-item-group title="分组2">
              <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <template slot="title">选项4</template>
              <el-menu-item index="1-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-menu"></i>
              <span slot="title">導航二</span>
            </template>
            <el-submenu index="2-4">
              <template slot="title">选项4</template>
              <el-menu-item index="2-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-setting"></i>
              <span slot="title">導航三</span>
            </template>
            <el-submenu index="3-4">
              <template slot="title">选项4</template>
              <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>
      <!--   側邊欄 結束   -->
      <!--   主體 開始   -->
      <el-container>
        <el-header style="font-size: 12px; border-bottom: 1px solid #ccc; line-height: 60px; display: flex">
          <div style="flex: 1;font-size: 20px">
            <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
          </div>
          <el-dropdown style="width: 70px; cursor: pointer">
            <span>王小虎</span><i class="el-icon-arrow-down" style="margin-left: 5px"></i>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>個人資料</el-dropdown-item>
              <el-dropdown-item>登出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-header>

        <el-main>
          <!--     查詢框 開始    -->
          <div style="padding: 10px 0">
            <el-input style="width: 200px;" suffix-icon="el-icon-search" placeholder="請輸入姓名"></el-input>
            <el-input style="width: 200px;" suffix-icon="el-icon-message" placeholder="請輸入信箱" class="ml-5"></el-input>
            <el-input style="width: 200px;" suffix-icon="el-icon-position" placeholder="請輸入地址" class="ml-5"></el-input>
            <el-button class="ml-5" type="primary">查詢</el-button>
          </div>
          <!--     查詢框 結束    -->
          <!--    新增按鈕 開始    -->
          <div style="margin: 10px 0">
            <el-button type="primary">新增<i class="el-icon-circle-plus-outline"></i></el-button>
            <el-button type="danger">批量刪除<i class="el-icon-remove-outline"></i></el-button>
            <el-button type="primary">導入<i class="el-icon-bottom"></i></el-button>
            <el-button type="primary">導入<i class="el-icon-top"></i></el-button>
          </div>
          <!--    新增按鈕 結束    -->

          <el-table :data="tableData" border stripe :header-cell-class-name="headerBg">
            <el-table-column align="center" prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column align="center" prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column align="center" prop="address" label="地址">
            </el-table-column>
            <el-table-column align="center" label="操作" >
              <template slot-scope="scope">
                <el-button type="success">編輯<i class="el-icon-edit"></i></el-button>
                <el-button type="danger">刪除<i class="el-icon-delete-solid"></i></el-button>
              </template>
            </el-table-column>
          </el-table>

          <!--     分頁開始     -->
          <div style="padding: 10px 0">
            <el-pagination
                :page-sizes="[5, 10, 15, 20]"
                :page-size="10"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
            </el-pagination>
          </div>
          <!--     分頁結束     -->
        </el-main>
      </el-container>
      <!--   主體 結束   -->
    </el-container>
</template>

<script>

export default {
  name: 'HomeView',
  data(){
    const item = {
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    };
    return {
      tableData: Array(10).fill(item),
      collapseBtnClass: 'el-icon-s-fold',
      isCollpase: false,
      sideWidth: 200,
      logoTextShow: true,
      headerBg: 'headerBg',
    }
  },
  methods: {
    collapse(){ //點擊收縮按鈕觸發
      this.isCollpase = !this.isCollpase
      if (this.isCollpase){ //收縮
        this.sideWidth = 64
        this.collapseBtnClass = 'el-icon-s-unfold'
        this.logoTextShow = false
      } else{ //展開
        this.sideWidth = 200
        this.collapseBtnClass = 'el-icon-s-fold'
        this.logoTextShow = true
      }
    }
  }
}
</script>

<style>
  .headerBg {
    background: #eee!important;
  }
</style>