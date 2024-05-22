<script setup>
import MenuItem from "@/components/common/MenuItem.vue"
import { Search, ShoppingCart } from "@element-plus/icons-vue"
import {useAuthStore} from "~/stores/auth.js";
import spaFetch from "~/plugins/fetch.js";


const route = useRoute()
const router = useRouter()
const auth = useAuthStore()
const {$apiUrl} = useNuxtApp()

const search = ref("")
const menu = ref([
    {
        isSubmenu: false,
        title: 'Trang chủ',
        link: '/'
    },
    {
        isSubmenu: true,
        title: 'Sản Phẩm ',
        link: '/category/xiaomi',
        children: [
            {img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Xiaomi_logo_%282021-%29.svg/2048px-Xiaomi_logo_%282021-%29.svg.png', link: '/category/xiaomi/'},
            {img: 'https://upload.wikimedia.org/wikipedia/commons/f/f1/Samsung_logo_blue.png',  link: '/category/samsung/'},
            {img: 'https://i.pinimg.com/originals/ca/86/fb/ca86fb1a51f4761d1246518ee7640010.png', link: '/category/apple/'},
            {img: 'https://upload.wikimedia.org/wikipedia/commons/1/13/OPPO_Logo_wiki.png',link: '/category/oppo/'},
            {img: 'https://upload.wikimedia.org/wikipedia/commons/9/91/Realme_logo.png', link: '/category/realme/'},
            {img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Redmi_Logo.svg/2560px-Redmi_Logo.svg.png', link: '/category/redmi/'},
        ],
        mainSubMenu: {img: 'https://cdn.tgdd.vn/Products/Images/42/279065/xiaomi-12t-thumb-bac-1-600x600.jpg',  link: '#'},
        colorBg: "bg-white",
        colorItemSM: "bg-grey"
    },
    {
        isSubmenu: false,
        title: 'Tin tức - Hướng dẫn',
        link: '#',
    },
    {
        isSubmenu: false,
        title: 'Youtube',
        link: '#',
    },
])

onMounted(() => {
    let prevScrollpos = window.pageYOffset;
    window.onscroll = function() {
        const currentScrollPos = window.pageYOffset;
        if (prevScrollpos > currentScrollPos && currentScrollPos > 120) {
            document.getElementById("navbar").style.top = "-140px";
        } else if (currentScrollPos <= 120) {
            document.getElementById("navbar").style.top = "0px"
        } else {
            document.getElementById("navbar").style.top = "-200px"
        }
        prevScrollpos = currentScrollPos;
    }
})
const handleClick = () => {
    router.push("/")
    console.log(route)
}

const logOut = () => {
    auth.deleteAuth()
    window.location.reload()
}

const getCart = () =>{
    const id = auth.$state.user && auth.$state.user.cart ? auth.$state.user.cart : null
    spaFetch()(`${$apiUrl.CART}${id}/`,{
        method: 'GET'
    }).then( res => {
        auth.setQuantityInCart(res.products.length)
    }).catch( error => {
        console.log("error", error.response)
    })
}

getCart()

watch(search, () => {
    router.push('/category/search/')
    auth.setSearch(search.value)
})
</script>

<template>
    <div class="h-screen relative">
        <div id="navbar">
            <div class="h-[40px] flex items-center justify-end p-2 bg-black text-white">
               <div v-if="!auth.$state.accessToken || !auth.$state.refreshToken">
                   <nuxt-link to="/login" class="cursor-pointer hover:underline hover:text-red-700">
                       Đăng nhập
                   </nuxt-link>
                   <el-divider direction="vertical"/>
                   <nuxt-link to="/register" class="cursor-pointer hover:underline hover:text-red-700">
                       Đăng ký
                   </nuxt-link>
               </div>
                <div v-else>
                    <span>
                        Xin chào, {{auth.$state.user.username}}
                    </span>
                    <el-divider direction="vertical"/>
                    <nuxt-link to="/myorder">
                       <span class="cursor-pointer hover:underline hover:text-red-700">
                            Đơn hàng của tôi
                       </span>
                    </nuxt-link>
                    <el-divider direction="vertical"/>
                    <span class="cursor-pointer hover:underline hover:text-red-700" @click="logOut">
                        Đăng xuất
                    </span>
                </div>
            </div>
            <div class="w-full h-[100px] flex flex-row justify-center items-center space-x-32">
                <div >
                    <img class="w-20 h-20" src="/Logodienthoai.jpg" alt="Logo Store">
                </div>
                <div class="w-1/3 border-solid border-4">
                    <el-input
                        v-model="search"
                        placeholder="Nhập từ khoá cần tìm"
                        class="input-with-select"
                        size="large"
                        :suffix-icon="Search"
                    >
                    </el-input>
                </div>
                <el-badge :value="auth.$state.quantityInCart" class="cursor-pointer hover:text-blue-600 transition duration-200" @click="$router.push('/cart')">
                    <el-icon size="40"><ShoppingCart/></el-icon>
                </el-badge>
            </div>
            <div class="flex justify-center text-xl font-bold relative bg-black">
                <MenuItem v-for="(item, index) in menu"
                          :key="index"
                          :item="item"
                          :class="item.isSubmenu ? 'menu-item-wrap' : ''"/>
            </div>
        </div>

        <div class=" mt-[200px]">
            <div v-if="route.href !== '/' "
                class="flex justify-center items-center">
                <div class="w-4/5 bg-black h-8 flex items-center pl-4 py-4 mt-4 text-white gap-x-4">
                    <span @click="handleClick"
                          class="cursor-pointer hover:underline-offset-1 hover:text-black" >
                        Trang chủ
                    </span>
                    <span>
                        >>
                    </span>
                </div>
            </div>
            <slot/>
        </div>
            </div>
</template>

<style lang="scss" >
.el-message{
    z-index: 9999 !important;
}
</style>