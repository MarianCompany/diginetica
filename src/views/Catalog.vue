<script>
import VHeader from "@/components/VHeader.vue";
import VMenu from "@/components/VMenu.vue";
import VProductList from "@/components/VProductList.vue";
import {defineComponent} from 'vue'

export default defineComponent({
    name: "Catalog",
    components: {
        VHeader,
        VMenu,
        VProductList,
    },
})
</script>

<template>
    <VHeader />
    <div class="catalog">
        <div class="container">
            <div class="catalog__wrapper">
                <div class="catalog__block">
                    <VMenu />
                </div>
                <div class="catalog__block">
                    <h2 class="catalog__title">
                        Название категории
                    </h2>
                    <VProductList class="catalog__product-list" />
                </div>
            </div>
        </div>
    </div>
</template>