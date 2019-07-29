<template>
  <el-container>
    <el-header>
      <el-row>
        <el-col :span='8'><img src="../assets/logo.png" alt=""></el-col>
        <el-col :span='8'><h1>电商后台管理系统</h1></el-col>
        <el-col :span='8' class="col3">恭喜上海前端36期月薪2W <a @click.prevent='logout' href="#">退出</a></el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside width="200px">
            <el-menu
              :router="true"
              :default-active="handleUrlPath()"
              background-color="#545c64"
              text-color="#fff"
              active-text-color="#ffd04b">
              <el-submenu index="1">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>用户管理</span>
                </template>
                <el-menu-item index="/users">用户列表</el-menu-item>
              </el-submenu>
              <el-submenu index="2">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>权限管理</span>
                </template>
                <el-menu-item index='/roles'>角色列表</el-menu-item>
                <el-menu-item index='/rights'>权限列表</el-menu-item>
              </el-submenu>
            </el-menu>
      </el-aside>
      <el-main>
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  methods: {
    logout () {
      this.$confirm('此操作将退出账户, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        localStorage.removeItem('token')
        this.$message({
          message: '退出成功',
          type: 'success',
          duration: 800
        })
        this.$router.push('/login')
      }).catch(() => {
        this.$message({
          message: '取消退出',
          type: 'info',
          duration: 800
        })
      })
    },
    handleUrlPath () {
      return this.$route.path
    }
  }
}
</script>

<style scoped lang='less'>
  .el-container {
    height: 100%;
  }
  .el-header {
    background-color: #b3c1cd;
    padding: 0;

    h1 {
      text-align: center;
      color: #fff;
      line-height: 60px;
      font-size: 26px;
    }

    .col3 {
      text-align: right;
      line-height: 60px;
      padding-right: 30px;
      a {
        color: #daa520
      }
    }
  }
  .el-aside {
    background-color: #545c64;
  }
  .el-main {
    background-color: #eaeef1;
  }
</style>
