<template>
  <el-container style="min-height: 100vh; border: 1px solid #eee">

    <el-aside :width="sideWidth+'px'" style="background-color: rgb(238, 241, 246);box-shadow: 2px 0 6px rgb(0 21 41/35%)">
      <el-menu :default-openeds="['1', '3']" style="min-height: 100%;overflow-x: hidden"
               background-color="rgb(48,65,86)"
               text-color="#fff"
               active-text-color="#ffd04b"
               :collapse-transition="false"
               :collapse="isCollapse"
      >
        <div style="height: 60px;line-height: 60px;text-align: center">
          <img src="../assets/logo.png" alt="" style="width: 25px;position: relative;top:7px;margin-right: 4px;margin-left: 4px">
          <b style="color: wheat" v-show="logoTextShow">图书管理系统</b>
        </div>
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-message"></i>
            <span slot="title">书籍借阅</span>
          </template>
        </el-submenu>
        <el-submenu index="2">
          <template slot="title">
            <i class="el-icon-menu"></i>
            <span slot="title">书籍归还</span>
          </template>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container>

      <el-header style=" font-size: 12px;border-bottom: 1px solid #ccc;line-height: 60px;display: flex">
        <div style="flex: 1;font-size:20px">
          <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
        </div>
        <el-dropdown style="width: 70px;cursor: pointer">
          <span>pxy</span><i class="el-icon-arrow-down" style="margin-left: 5px"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>
              <i class="el-icon-warning-outline"></i>个人信息
            </el-dropdown-item>
            <el-dropdown-item>
              <i class="el-icon-switch-button"></i>登出
            </el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-header>

      <el-main>
        <!-- 分页栏 -->
        <el-breadcrumb separator-class="el-icon-arrow-right" style="padding: 5px 0">
          <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
          <el-breadcrumb-item>书籍借阅</el-breadcrumb-item>
        </el-breadcrumb>

        <!-- 查询框 -->
        <div style="padding: 10px 0">
          <el-input style="width: 200px;margin-right: 5px" placeholder="条形码索书号" prefix-icon="el-icon-document-copy"></el-input>
          <el-button type="primary" @click="load" style="margin-right: 25px">精确搜索</el-button>
          <el-input style="width: 150px;margin-right: 5px" placeholder="书名" prefix-icon="el-icon-notebook-2" v-model="bookName"></el-input>
          <el-input style="width: 100px;margin-right: 5px" placeholder="作者" prefix-icon="el-icon-user" v-model="author"></el-input>
          <el-input style="width: 100px;margin-right: 5px" placeholder="出版商" prefix-icon="el-icon-house" v-model="publish"></el-input>
          <el-input style="width: 100px;margin-right: 5px" placeholder="ISBN号" prefix-icon="el-icon-paperclip" v-model="ISBN"></el-input>
          <el-button type="primary" @click="load">模糊搜索</el-button>
        </div>
        <!--    学生界面用不到，管理员界面可添加
        <div style="padding: 10px 0">
          <el-button type="primary">新增 <i class="el-icon-circle-plus-outline"></i></el-button>
          <el-button type="danger">批量删除 <i class="el-icon-remove-outline"></i></el-button>
          <el-button type="primary">导入 <i class="el-icon-download"></i></el-button>
          <el-button type="primary">导出 <i class="el-icon-upload2"></i></el-button>
        </div>
        -->


        <el-table :data="tableData" border stripe>
          <el-table-column prop="bookName" label="书籍名称" width="140">
          </el-table-column>
          <el-table-column prop="author" label="作者" width="120">
          </el-table-column>
          <el-table-column prop="publish" label="出版商">
          </el-table-column>
          <el-table-column prop="ISBN" label="ISBN号"></el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button type="success" @click="borrow">借阅 <i class="el-icon-reading"></i></el-button>
            </template>
          </el-table-column>
        </el-table>

        <div style="padding: 10px 0">
          <el-pagination
              :current-page="pageNum"
              :page-sizes="[5, 10, 20, 50]"
              :page-size="pageSize"
              layout="total, sizes, prev, pager, next, jumper"
              :total="total">
          </el-pagination>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'bookBorrow',
  data() {
    const item = {
      bookName:"1",
      author:"pxy",
      publish:"abc",
      ISBN:"ddd"
    };
    return {
      tableData:Array(10).fill(item),
      total:0,
      collapseBtnClass:'el-icon-s-fold',
      isCollapse:false,
      sideWidth:200,
      logoTextShow:true,
      pageNum:1,
      pageSize:5,
      bookName:"",
      author:"",
      publish:"",
      ISBN:""
    }
  },
  methods:{
    collapse(){//点击收缩时触发
        this.isCollapse = !this.isCollapse;
        if (this.isCollapse){//收缩状态
          this.sideWidth=64;
          this.collapseBtnClass='el-icon-s-unfold'
          this.logoTextShow=false
        }else{//展开
          this.sideWidth=200
          this.collapseBtnClass='el-icon-s-fold'
          this.logoTextShow=true
        }
    },
    load(){//点击搜索时触发
      //request.get("http://localhost:#/user/page?pageNum="
      //    +this.pageNum+"&pageSize="+this.pageSize+"&bookName="+this.bookName
      //    +"&author="+this.author+"&publish="+this.publish+"&ISBN="+this.ISBN).then(res => res.json())
    },
    borrow(){//点击借阅时触发

    }
  }
}
</script>
