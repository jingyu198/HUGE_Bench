<script lang="ts" setup>
import { ElIcon } from 'element-plus'
import { SuccessFilled } from '@element-plus/icons-vue'

const logo = {
    name: "Template",
    link: "#",
}

const more_paper = {
    "ExtDM": {
        name: "ExtDM - CVPR 2024",
        link: "https://zzcheng.top/ExtDM/",
    },
    "MPOT": {
        name: "MPOT - ICCV 2023",
        link: "https://zzcheng.top/MPOT/",
    },
    "ControlNet": {
        name: "ControlNet - ICCV 2023",
        link: "https://github.com/lllyasviel/ControlNet",
    }
}
</script>

<template>
    <el-affix :offset="0" :style="{ width: '100%' }">
        <el-menu
            default-active="1"
            class="el-menu-demo"
            mode="horizontal"
            :ellipsis="false"
        >
            <el-menu-item index="1">
                <el-icon :size="20"><SuccessFilled /></el-icon>
                <a :href="logo.link">{{ logo.name }}</a>
            </el-menu-item>

            <el-sub-menu index="2">
                <template #title>More</template>
                <el-menu-item index="2-1">
                    <a :href="more_paper.ExtDM.link">{{ more_paper.ExtDM.name }}</a>
                </el-menu-item>
                <el-menu-item index="2-2">
                    <a :href="more_paper.MPOT.link">{{ more_paper.MPOT.name }}</a>
                </el-menu-item>
                <el-menu-item index="2-3">
                    <a :href="more_paper.ControlNet.link">{{ more_paper.ControlNet.name }}</a>
                </el-menu-item>
            </el-sub-menu>
        </el-menu>
    </el-affix>
</template>

<style>
.el-menu {
    background: none;
}

.el-menu--popup {
    min-width: 100%;
}

.el-affix--fixed {
    box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
    background-image: radial-gradient(#ffffffca 1px, #ffffff 1px);
    background-size: 3px 3px;
}

.el-header {
    --el-header-height: 50px;
}
</style>

<style scoped>
.el-menu--horizontal > .el-menu-item:nth-child(1) {
    margin-right: auto;
}

.el-menu--horizontal {
    --el-menu-horizontal-height: 50px;
}

a:hover {
    color: inherit;
    border-bottom: none;
}

a {
    text-decoration: none;
    color: inherit;
}
</style>
