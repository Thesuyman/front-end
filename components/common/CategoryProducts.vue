<script setup>

import {CaretRight} from "@element-plus/icons-vue";
import {SwiperSlide} from "swiper/vue";
import MenuNewProducts from "~/components/common/MenuNewProducts.vue";
import MenuHotDealProducts from "~/components/common/MenuHotDealProducts.vue";
import SamsungProduct from "~/components/common/SamsungProduct.vue";
import OtherProduct from "~/components/common/OtherProduct.vue";


const props = defineProps({
    visible: {
        type: Boolean,
        default() {
            return false
        }
    }
})

const categorys = ref ([
    {
        img: 'https://png.pngtree.com/png-vector/20220628/ourmid/pngtree-smartphone-logo-design-blue-contact-png-image_5547061.png',
        img1: 'https://png.pngtree.com/png-vector/20220628/ourmid/pngtree-smartphone-logo-design-blue-contact-png-image_5547061.png',
        name: 'Chọn Hãng Điện Thoại',

        categoruDrops: [
            {
                content: 'SamSung',
                link: '/category/samsung'
            },
            {
                content: 'Xiaomi',
                link: '/category/xiaomi'
            },
            {
                content: 'Apple',
                link: '/category/apple'
            },
            {
                content: 'Oppo',
                link: '/category/oppo'
            },
            {
                content: 'RealMe',
                link: '/category/realme'
            },
            {
                content: 'Redmi',
                link: '/category/redmi'
            },
        ]

    },
])
</script>

<template>
    <div class="w-full mt-4 flex">
        <div class="w-1/6 bg-white z-100  ">
            <div class="p-3 bg-black font-semibold text-white">
                Danh mục
            </div>

            <div v-for="(category, index) in categorys"
                     :key="index"
                 class="p-3 bg-gray-100 flex items-center gap-4 cursor-pointer relative category-wrap justify-between hover:bg-red-600 hover:text-white flex-items-hover">
                <div class="flex items-center gap-3">
                    <img class="w-6 h-6 img" :src="category.img" alt="">
                    <img class="w-6 h-6 img1 hidden" :src="category.img1" alt="">
                    {{category.name ? category.name : ''}}
                </div>
                <el-icon class="" ><CaretRight/></el-icon>
                <div class="w-full bg-white absolute left-full top-0 hidden category-drop">
                    <div v-for="(categoryDrop, index ) in category.categoruDrops"
                         :key="index"
                         class="w-full bg-gray-100 p-3 flex items-center gap-4 cursor-pointer relative justify-between category-drop-item z-[9999999]" @click="$router.push(categoryDrop.link)">
                        <div>
                            {{categoryDrop.content}}
                        </div>
                    </div>
                </div>
            </div>

            <div class="w-full mt-5 hover:mt-10 border-solid border-gray-500 border-2 rounded-xl p-4">
                <img class="w-full h-full rounded-xl" src="https://dienthoaigiakho.vn/_next/image?url=https%3A%2F%2Fcdn.dienthoaigiakho.vn%2Fphotos%2F1709620515170-600x180_Sub-Banner-Redmi-Note-13.jpg&w=3840&q=75" alt="">
            </div>
            <div class="w-full mt-5 hover:mt-10 border-solid border-gray-500 border-2 rounded-xl p-4">
                <img class="w-full h-full rounded-xl" src="https://guardian.ng/wp-content/uploads/2023/03/1.-Redmi-Note-12-Series-2048x1152.jpg" alt="">
            </div>
        </div>

        <div class="w-5/6 bg-white text-fuchsia-400 pl-4 flex flex-col gap-y-3">
           <slot/>
        </div>

    </div>
</template>

<style lang="scss" scoped>
.category-wrap{
    .category-drop{
        background-color: white;
        color: black;
        .category-drop-1{
            .category-drop-1-item{
                background-color: white;
                color: black;
                &:hover{
                    background-color: rgb(220 38 38);
                    color: white;
                }
            }
        }

        .category-drop-item{

            &:hover{
                background-color: rgb(220 38 38);
                color: white;
                .category-drop-1{
                    display: block;
                }
            }
        }

    }

    &:hover{
        .category-drop{
            display: flex;
            flex-direction: column;
        }
        .img{
            display: none;
        }
        .img1{
            display: block;
        }
    }
}

</style>