<template>
    <el-container style="height: 500px; border: 1px solid #eee">
        <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
            <!--        <el-menu :default-openeds="['1']" :default-active="'1-2'">-->
            <!--          <el-submenu index="1">-->
            <!--            <template slot="title"><i class="el-icon-setting"></i>导航一</template>-->
            <!--            <el-submenu index="1-1">-->
            <!--              <template slot="title"><i class="el-icon-add-location"></i>选项1</template>-->
            <!--              <el-menu-item><i class="el-icon-setting"></i>选项1-2-1</el-menu-item>-->
            <!--            </el-submenu>-->
            <!--            <el-submenu index="1-2">-->
            <!--              <template slot="title"><i class="el-icon-setting"></i>选项2</template>-->
            <!--            </el-submenu>-->
            <!--            <el-menu-item index="1-3">选项1-3</el-menu-item>-->
            <!--          </el-submenu>-->
            <!--        </el-menu>-->
            <el-menu router :default-openeds="['0','1']">
                <el-submenu v-for="(item,index) in $router.options.routes" :index="index+''" v-if="item.show!=false">
                    <template slot="title"><i class="el-icon-setting"></i>{{item.name}}</template>
                    <el-menu-item v-for="(item2,index2) in item.children" :index="item2.path" :class="item2.path==$route.path?'is-active':''">
                        <template slot="title"><i class="el-icon-setting"></i>{{item2.name}}</template>
                    </el-menu-item>
                </el-submenu>
            </el-menu>
        </el-aside>
        <el-container>
            <el-header style="text-align: right; font-size: 12px">
                <el-dropdown>
                    <i class="el-icon-setting" style="margin-right: 15px"></i>
                    <el-dropdown-menu slot="dropdown">
                        <el-dropdown-item>查看</el-dropdown-item>
                        <el-dropdown-item>新增</el-dropdown-item>
                        <el-dropdown-item>删除</el-dropdown-item>
                    </el-dropdown-menu>
                </el-dropdown>
                <span>王小虎</span>
            </el-header>

            <el-main>
                <router-view></router-view>
            </el-main>
        </el-container>
    </el-container>
</template>

<script>
    export default {
        name: "index"
    }
</script>

<style scoped>

</style>
