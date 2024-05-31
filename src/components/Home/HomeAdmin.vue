<template>
  <el-container class="home-container">
    <!-- 头部区域 -->
    <el-header>
      <div class="header-with-padding">
        <img :src="require('@/assets/images/logo.png')" alt="" width="30" height="30"/>
        <span>欢迎登录图书管理系统</span>
        <span style="color: #ccc; font-size: 16px">系统管理人员页面</span>
      </div>
      <div>
        <a href="https://github.com/zljdgit/LibMngSys" title="GitHub前端源码地址" target="_blank"
           style="margin-right:10px">
          <svg t="1717052261316" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="6772" width="35" height="35">
            <path d="M511.6 76.3C264.3 76.2 64 276.4 64 523.5 64 718.9 189.3 885 363.8 946c23.5 5.9 19.9-10.8 19.9-22.2v-77.5c-135.7 15.9-141.2-73.9-150.3-88.9C215 726 171.5 718 184.5 703c30.9-15.9 62.4 4 98.9 57.9 26.4 39.1 77.9 32.5 104 26 5.7-23.5 17.9-44.5 34.7-60.8-140.6-25.2-199.2-111-199.2-213 0-49.5 16.3-95 48.3-131.7-20.4-60.5 1.9-112.3 4.9-120 58.1-5.2 118.5 41.6 123.2 45.3 33-8.9 70.7-13.6 112.9-13.6 42.4 0 80.2 4.9 113.5 13.9 11.3-8.6 67.3-48.8 121.3-43.9 2.9 7.7 24.7 58.3 5.5 118 32.4 36.8 48.9 82.7 48.9 132.3 0 102.2-59 188.1-200 212.9 23.5 23.2 38.1 55.4 38.1 91v112.5c0.8 9 0 17.9 15 17.9 177.1-59.7 304.6-227 304.6-424.1 0-247.2-200.4-447.3-447.5-447.3z" p-id="6773" fill="#FFC000">
            </path>
          </svg>
        </a>
        <a href="https://github.com/zljdgit/LibMngSys_backend" title="GitHub后端源码地址" target="_blank"
           style="margin-right:10px">
          <svg t="1686048645435" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
               p-id="1265" width="30" height="30">
            <path
                d="M0 524.992q0 166.016 95.488 298.496t247.488 185.504q6.016 0.992 10.016 0.992t6.496-1.504 4-3.008 2.016-4.992 0.512-4.992v-100.512q-36.992 4-66.016-0.512t-45.504-14.016-28.992-23.488-16.992-25.504-8.992-24-5.504-14.496q-8.992-15.008-27.008-27.488t-27.008-20-2.016-14.496q50.016-26.016 112.992 66.016 34.016 51.008 119.008 30.016 10.016-40.992 40-70.016Q293.984 736 237.984 670.976t-56-158.016q0-87.008 55.008-151.008-22.016-64.992 6.016-136.992 28.992-2.016 64.992 11.488t50.496 23.008 25.504 17.504q56.992-16 128.512-16t129.504 16q12.992-8.992 28.992-19.008t48.992-21.504 60.992-9.504q27.008 71.008 7.008 135.008 56 64 56 151.008 0 92.992-56.992 158.496t-172 85.504q43.008 43.008 43.008 104v128.992q0 0.992 0.992 3.008 0 6.016 0.512 8.992t4.512 6.016 12 3.008q152.992-52 250.496-185.504t97.504-300.512q0-104-40.512-199.008t-108.992-163.488-163.488-108.992T512.032 12.96 313.024 53.472 149.536 162.464t-108.992 163.488-40.512 199.008z"
                p-id="1266" fill="#1296db"></path>
          </svg>
        </a>
        <div>
          <el-avatar
            src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"
            :size="35"
            style="margin-right: 10px"
          ></el-avatar>
        </div>
        <div class="user">管理员:{{ this.admin.adminName }}</div>
        <el-button type="info" @click="logout">退出</el-button>
      </div>
    </el-header>
    <!-- 页面主体区域 -->
    <el-container>
      <!-- 侧边栏 -->
      <el-aside :width="isCollapse ? '64px' : '200px'">
        <div class="toggle-button" @click="toggleCollapse">|||</div>
        <!-- 侧边栏菜单区域 -->
        <el-menu :default-active="activePath" class="el-menu-vertical-demo" background-color="#545c64" text-color="#fff"
                 active-text-color="#ffd04b" :router="true" :collapse="isCollapse" :collapse-transition="false" style="height: 100%;">
          <el-menu-item index="bookmanage" @click="saveNavState('bookmanage')">
            <i class="el-icon-notebook-1"></i>
            <span slo="title">书籍管理</span>
          </el-menu-item>
<!--          <el-menu-item index="booktype" @click="saveNavState('booktype')">
            <i class="el-icon-notebook-2"></i>
            <span slot="title">书籍类型</span>
          </el-menu-item>-->
          <el-menu-item
            index="statementmanage"
            @click="saveNavState('statementmanage')"
          >
            <i class="el-icon-bank-card"></i>
            <span slot="title">借阅证管理</span>
          </el-menu-item>
          <el-menu-item
            index="statementsearch"
            @click="saveNavState('statementsearch')"
          >
            <i class="el-icon-search"></i>
            <span slot="title">借阅信息查询</span>
          </el-menu-item>
          <el-menu-item
            index="statementrulemanage"
            @click="saveNavState('statementrulemanage')"
          >
            <i class="el-icon-key"></i>
            <span slot="title">借阅规则管理</span>
          </el-menu-item>
          <el-menu-item
            index="bookadminmanage"
            @click="saveNavState('bookadminmanage')"
          >
            <i class="el-icon-user-solid"></i>
            <span slot="title">图书管理员管理</span>
          </el-menu-item>
          <el-menu-item
            index="adminmanage"
            @click="saveNavState('adminmanage')"
          >
            <i class="el-icon-s-tools"></i>
            <span slot="title">系统管理</span>
          </el-menu-item>
          <el-menu-item
              index="intelligent_analysis"
              @click="saveNavState('intelligent_analysis')"
          >
            <i class="el-icon-data-line"></i>
            <span slot="title">智能分析</span>
          </el-menu-item>
        </el-menu>
      </el-aside>
      <!-- 右侧内容主体 -->
      <el-main>
        <!-- 路由占位符 -->
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

  <script>
export default {
  data() {
    return {
      //左侧菜单数据
      menulist: [],
      iconsObj: {
        125: "iconfont icon-user",
        103: "iconfont icon-tijikongjian",
        101: "iconfont icon-shangpin",
        102: "iconfont icon-danju",
        145: "iconfont icon-baobiao",
      },
      //是否折叠
      isCollapse: false,
      //被激活的链接地址
      activePath: "",
      admin: {
        adminId: Number,
        status: Number,
        adminName: "",
        username: "",
        password: "",
        createTime: "",
        updateTime: "",
      },
    };
  },
  async created() {
    // this.getMenuList();
    this.activePath = window.sessionStorage.getItem("activePath");
    // console.log(this.activePath)
    // 先获取sessionStorage中的id
    const stringId = window.sessionStorage.getItem("adminId");
    const id = parseInt(stringId);
    this.admin.adminId = id;
    const { data: res } = await this.$http.post("admin/getData", this.admin);
    this.admin = res.data;
  },
  methods: {
    logout() {
      window.sessionStorage.clear();
      this.$router.push("/loginadmin");
    },

    //点击按钮，切换菜单的折叠与展开
    toggleCollapse() {
      this.isCollapse = !this.isCollapse;
    },
    //保存链接的激活状态
    saveNavState(activePath) {
      // console.log("first")
      window.sessionStorage.setItem("activePath", activePath);
      this.activePath = activePath;
      // console.log(this.activePath);
    },
  },
};
</script>

<style lang="less" scoped>
.footer {
  position: fixed;
  bottom: 0px;
  left: 40%;
  color:#ccc;
  a {
    color:#ccc;
  }
}

.header-with-padding {
  padding-left: 12px; /* 根据需要调整左侧空白区域的大小 */
}
.home-container {
  height: 100%;
}
.el-header {
  background-color: rgb(34, 34, 34);
  display: flex;
  justify-content: space-between;
  padding-left: 0px;
  align-items: center;
  color: #fff;
  font-size: 20px;
  border-radius: 10px;
  > div {
    display: flex;
    align-items: center;
    span {
      margin-left: 15px;
    }
  }
}
.el-aside {
  background-color: #fff;
  .el-menu {
    border-right: none;
  }
}
.el-main {
  background-color: #eaedf1;
  padding: 20px;
}
.iconfont {
  margin-right: 10px;
}
.toggle-button {
  background-color: #4a5064;
  font-size: 10px;
  line-height: 24px;
  color: #fff;
  text-align: center;
  //设置文字之间的间距
  letter-spacing: 0.2em;
  cursor: pointer;
}
.user {
  margin-right: 15px;
  color: #ccc;
  font-size: 16px;
}
.el-menu-item:hover {
  background-color: rgb(51, 122, 183) !important;
}
// .el-menu-item{
//   color:rgb(135, 206, 235) !important;
// }
</style>
