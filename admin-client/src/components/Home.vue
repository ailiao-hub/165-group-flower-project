<template>
    <el-container class="home-container">
        <!-- 头部部分 -->
        <el-header>
            <el-row :gutter="20">
                <el-col :span="20">
                    <div class="grid-content bg-purple"><h3>花店后台管理系统</h3></div>
                </el-col>
                <el-col :span="4">
                    <div class="grid-content bg-purple user">

                        <b @click="$router.push('/message')" class="minfo">消息中心</b>
                        <span>Hi，{{user.user}}</span><i class="iconfont icon-zhuxiaologout11" @click="logout"
                                                        title="退出登录"></i>
                    </div>
                </el-col>
            </el-row>

        </el-header>
        <!-- 主要内容 -->
        <el-container>
            <!-- 侧边栏菜单 -->
            <el-aside :width="fold?'64px':'200px'">
                <!-- 侧边栏菜单区域 -->
                <el-menu :collapse-transition="false" router :collapse="fold" background-color="#545c64"
                         text-color="#fff" active-text-color="#ffd04b" unique-opened>
                    <!-- 折叠菜单 -->
                    <div class="fold" :title="title" @click="doFold">
                        <span :class="fold ? 'el-icon-s-unfold' : 'el-icon-s-fold'"></span>
                    </div>
                    <!--el-submenu 一级菜单 -->
                    <el-submenu index="1">
                        <!-- template 一级菜单的模板区域 -->
                        <template slot="title">
                            <!-- i 图标 -->
                            <i class="el-icon-user"></i>
                            <!--span 文本 -->
                            <span>用户管理</span>
                        </template>
                        <!-- 二级菜单 -->
                        <el-menu-item index="/users">
                            <span>用户列表</span>
                        </el-menu-item>
                        <!--                        <el-menu-item index="/member">-->
                        <!--                            <span>会员列表</span>-->
                        <!--                        </el-menu-item>-->
                    </el-submenu>

                    <el-submenu index="2">
                        <template slot="title">
                            <i class="iconfont icon-cangku"></i>
                            <span>仓库管理</span>
                        </template>
                        <el-menu-item index="/home/order/list">
                            <span>仓库列表</span>
                        </el-menu-item>
                    </el-submenu>
                    <el-submenu index="3">
                        <template slot="title">
                            <i class="el-icon-notebook-2"></i>
                            <span>商品管理</span>
                        </template>
                        <el-menu-item index="/booklist">
                            <span>商品列表</span>
                        </el-menu-item>
                        <!--                        <el-menu-item index="/bookclassify">-->
                        <!--                            <span>书籍分类</span>-->
                        <!--                        </el-menu-item>-->
                    </el-submenu>

                    <el-submenu index="4">
                        <template slot="title">
                            <i class="el-icon-s-order"></i>
                            <span>订单管理</span>
                        </template>
                        <el-menu-item index="/home/order/list">
                            <span>订单列表</span>
                        </el-menu-item>

                    </el-submenu>
                    <el-submenu index="5">
                        <template slot="title">
                            <i class="el-icon-pie-chart"></i>
                            <span>数据统计</span>
                        </template>
                        <el-menu-item index="/home/order/total">
                            <span>数据分析</span>
                        </el-menu-item>
                    </el-submenu>
                    <el-submenu index="6">
                        <template slot="title">
                            <i class="el-icon-setting"></i>
                            <span>设置</span>
                        </template>
                        <el-menu-item index="/home/adminSet">
                            <span>管理员设置</span>
                        </el-menu-item>
                    </el-submenu>
                </el-menu>
            </el-aside>
            <!--  主体内容-->
            <el-main>
                <!--路由导航-->
                <div>
                    <router-view></router-view>
                </div>


            </el-main>
        </el-container>
    </el-container>

</template>

<script>

    export default {
        data() {
            return {
                title: "折叠",
                fold: false,
                active: {
                    color: "#ffd04b"
                },
                user: {user: 'admin'}

            }
        },
        methods: {
            //退出登录
            logout() {
                window.sessionStorage.removeItem('user')
                this.$router.push('/login')
            },
            //折叠
            doFold() {
                this.title = this.fold ? "折叠" : "展开";
                this.fold = !this.fold;
            },
        },
        created() {
            this.$axios({
                method: 'post',
                url: '/api/user/login',
                data: {phone: 110, password: 123123}
            }).then(result => {
                console.log(result)
            })
        }
    }
</script>

<style scoped="scoped">
    .minfo {
        margin-right: 10px;
    }

    .minfo:hover {
        color: #409EFF;
        cursor: pointer;
    }

    header {
        width: 100%;
        background-color: #545c64;
    }

    .el-badge {
        margin-right: 20px;
    }

    .user {
        margin-top: 20px;
    }

    header h3, .user {
        color: #FFFFFF;
    }

    .fold {
        background-color: #CCCCCC;
        text-align: center;
        cursor: pointer;
    }

    .home-container {
        height: 100%;
    }

    .el-aside {
        background-color: #545c64;
        height: 100%;

    }

    .el-menu {
        border: none;
    }

    .el-main {
        background-color: #FFFFCC;
        height: 100%;
    }

    .statu {
        color: #ffd04b;
    }

    .foods-wrapper {
        height: 1px;
    }
</style>
