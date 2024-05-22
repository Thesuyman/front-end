<script setup>
import MenuNewProducts from "~/components/common/MenuNewProducts.vue";
import CategoryProducts from "~/components/common/CategoryProducts.vue";
import MenuHotDealProducts from "~/components/common/MenuHotDealProducts.vue";
import OtherProduct from "~/components/common/OtherProduct.vue";
import SamsungProduct from "~/components/common/SamsungProduct.vue";

const intervalImg = ref()
const checkInterval = ref(false)
const handleClickItem = (index, isInterval = false) => {
    if(!isInterval){
        checkInterval.value = false
        clearInterval(intervalImg.value)
    }
    const newsNavs = document.getElementsByClassName("news-nav")
    document.getElementById(`slide${index + 1}`).click()
    if (newsNavs && newsNavs.length > 0) {
        for (let i = 0; i < newsNavs.length; i++) {
            if (i === index) {
                newsNavs[i].classList.add('is-active');
            } else {
                newsNavs[i].classList.remove('is-active');
            }
        }
    }
}

onMounted(() => {
    checkInterval.value = true
    intervalImg.value = setInterval(() => {
       if(checkInterval.value){
           handleClickItem(1, true)
       }
        setTimeout(() => {
           if(checkInterval.value){
               handleClickItem(2, true)
           }
            setTimeout(() => {
                if(checkInterval.value){
                    handleClickItem(0, true)
                }
            }, 2000)
        }, 2000)
    }, 6000)
})

onUnmounted(() => {
    clearInterval(intervalImg.value)
})
</script>

<template>
    <div class="flex flex-col">
        <div class="picture-paddyfield h-[600px]">
            <div class="khoi_anh">
                <div id="homepage-slider" class="st-slider h-full w-full">
                    <input type="radio" class="cs_anchor radio" name="slider" id="slide1"/>
                    <input type="radio" class="cs_anchor radio" name="slider" id="slide2"/>
                    <input type="radio" class="cs_anchor radio" name="slider" id="slide3"/>
                    <div class="images">
                        <div class="images-inner">
                            <div class="image-slide">
                                <img class="image"
                                     src="https://shopdunk.com/images/thumbs/0022013_banner%20iphone%2015%20pro%20max%20TH_PC_1600.jpeg">
                            </div>
                            <div class="image-slide">
                                <img class="image"
                                     src="https://cdn2.cellphones.com.vn/insecure/rs:fill:0:358/q:90/plain/https://cellphones.com.vn/media/catalog/product/x/i/xiaomi_14_12gb_256gb_-_3.png">
                            </div>
                            <div class="image-slide">
                                <img class="image"
                                     src="https://www.techone.vn/wp-content/uploads/2022/04/banner-01.jpg">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="w-full h-12 bg-black text-white text-xl flex justify-around items-end">
            <div class="w-[240px] h-full news-nav is-active" @click="handleClickItem(0)">
                <div class="w-full h-full flex cursor-pointer justify-center items-center rounded-t-2xl hover:text-red-500">
                   SẢN PHẨM MỚI
                </div>
            </div>

            <div class="w-[240px] h-full news-nav" @click="handleClickItem(1)">
                <div class="w-full h-full flex cursor-pointer justify-center items-center rounded-t-2xl hover:text-red-500">
                    Sản phẩm nổi bật
                </div>
            </div>
            <div class="w-[240px] h-full news-nav" @click="handleClickItem(2)">
                <div class="w-full h-full flex cursor-pointer justify-center items-center rounded-t-2xl hover:text-red-500">
                    Chương trình đặc biệt
                </div>
            </div>
        </div>

        <div class="w-4/5 flex flex-col items-center justify-center mt-4 mx-auto">
            <div class=" w-full bg-black h-10 flex ">
                <div class="w-1/6 bg-black flex items-center justify-center">
                    <span class="text-xl font-bold flex text-white">
                        Hàng mới về
                    </span>
                </div>
            </div>
            <div class="w-full">
                <MenuNewProducts/>
                <CategoryProducts>
                    <MenuHotDealProducts/>
                    <MenuGundamProducts/>
                    <MenuT1Products/>
                </CategoryProducts>


            </div>
        </div>
    </div>
</template>

<style lang="scss">

</style>
