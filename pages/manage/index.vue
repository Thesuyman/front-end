<script setup>
import TableProduct from "~/components/manage/TableProduct.vue";

definePageMeta({
    layout: "admin",
    middleware: "auth"
})

import TableOrder from "~/components/manage/TableOrder.vue";
import TableUser from "~/components/manage/TableUser.vue";
import {useAuthStore} from "~/stores/auth.js";

const active = ref('1')
const auth = useAuthStore()

const logOut = () => {
    auth.deleteAuth()
    window.location.reload()
}

const handleChange = (key) => {
    console.log(key)
    active.value = key
}
</script>

<template>
    <div class="w-full h-screen">
        <div class="w-full h-full flex">
            <el-menu
                active-text-color="#ffd04b"
                background-color="#000"
                default-active="1"
                text-color="#fff"
                class="w-60 h-full"
                @select="handleChange"
            >
                <el-menu-item class="mb-6" index="0">
                    <img class="h-32 mt-8 ml-6"
                         src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSAkFjZctCsvHceEOdHnUzbkgo3PR1m7jXRKYqR83R9Fw&s"
                         alt="">
                </el-menu-item>
                <el-menu-item index="1">
                    <span>Quản lý sản phẩm</span>
                </el-menu-item>
                <el-menu-item index="2">
                    <span>Quản lý đơn hàng</span>
                </el-menu-item>
                <el-menu-item index="3">
                    <span>Quản lý tài khoản</span>
                </el-menu-item>
                <el-menu-item>
                    <span class="cursor-pointer hover:underline hover:text-red-700 mt-20 ml-2 text-white" @click="logOut">
                        Đăng xuất
                    </span>
                </el-menu-item>
            </el-menu>

            <TableProduct v-if="active === '1'" class="flex-1 overflow-auto"/>
            <TableOrder v-if="active === '2'" class="flex-1 overflow-auto"/>
            <TableUser v-if="active === '3'" class="flex-1 overflow-auto"/>
        </div>
    </div>
</template>

<style lang="scss">

</style>