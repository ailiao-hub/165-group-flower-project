<template>
    <div>
        <!--   顶部导航栏   -->
        <el-menu
                router
                :default-active="activeIndex"
                mode="horizontal"
                active-text-color="#FB7299"

        >
            <!--  导航栏菜单项  -->
            <el-menu-item><img width="90" src="../assets/image/logo.png"></el-menu-item>
            <el-menu-item index="/index">首页</el-menu-item>
            <el-menu-item index="/class">分类</el-menu-item>
            <el-menu-item index="/class">花语大全</el-menu-item>

            <el-menu-item index="/customer-service">联系我们</el-menu-item>


            <el-submenu index="2" style="float: right">
                <template slot="title">
                    <el-avatar size="medium" :src="avatarSrc"></el-avatar>
                    <span> 我的信息</span>
                </template>
                <el-menu-item index="/user">
                    <i class="el-icon-user"></i>
                    <span>个人中心</span>
                </el-menu-item>
                <el-menu-item index="2-2">
                    <i class="el-icon-s-order"></i>
                    <span>订单管理</span>

                </el-menu-item>
                <el-menu-item index="2-3">选项3</el-menu-item>
            </el-submenu>
            <el-menu-item index="/reply" style="float: right">消息中心</el-menu-item>
            <el-menu-item index="/cart" style="float: right">购物车</el-menu-item>
            <el-menu-item index="/member" style="float: right">店铺会员</el-menu-item>
            <el-menu-item style="float: right">
                <el-input placeholder="商品搜索">
                    <el-button slot="append" icon="el-icon-search"></el-button>
                </el-input>
            </el-menu-item>
        </el-menu>

        <!--  路由 -->
        <div id="body">
            <router-view></router-view>
        </div>
    </div>
</template>


<script>
    export default {
        data() {
            return {
                activeIndex: "/home",
                userinfo: {},
                avatarSrc: require('../assets/image/avatar.jpg'),

            };
        },
        methods: {
            getUser() {
                this.$axios({
                    url: "/api/user/login",
                    method: "post",
                    params: {phone: "110", password: "123123"},
                }).then((result) => {
                    console.log(result);
                });
            },
        },
        created() {
            this.getUser();
        },
    };
</script>

<style scoped>
    #body {
        margin: 0% auto;
        width: 80%;
    }


</style>