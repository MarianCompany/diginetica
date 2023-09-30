<script>
import {defineComponent} from 'vue'
import Fire from "@/components/icons/Fire.vue";
import ProductImgDefault from "./icons/ProductImgDefault.vue";

export default defineComponent({
    name: "VProductItem",
    components: {ProductImgDefault, Fire},
    props: {
        productItem: {
            type: Object,
            required: true,
        }
    },
    computed: {
        isProductOnDiscount () {
            return this.productItem.discountPercent !== -1;
        },

        formattedPrice () {
            return this.productItem.price.toLocaleString('ru-RU');
        },

        formattedOldPrice () {
            return this.productItem.oldPrice.toLocaleString('ru-RU');
        },
    }
})
</script>

<template>
    <div
        :class="{
            'product_not-available': !productItem.isAvailable,
        }"
        class="product"
    >
        <div class="product__preview">
            <div v-if="productItem.isBestseller" class="product__bestseller">
                <div class="label label_with-img label_grey-bordered">
                    <p class="label__text">
                        Хит продаж
                    </p>
                    <div class="label__img-wrap">
                        <Fire class="label__img" />
                    </div>
                </div>
            </div>
            <div class="product__img-wrap">
                <ProductImgDefault class="product__img" />
            </div>
            <div v-if="isProductOnDiscount" class="product__discount">
                <div class="label label_blue">
                    <p class="label__text label__text_white label__text_bold">
                        {{ productItem.discountPercent }}%
                    </p>
                </div>
            </div>
        </div>
        <div class="product__body">
            <div class="product__brand">
                <p class="product__brand-text">
                    {{ productItem.brand }}
                </p>
            </div>
            <div class="product__name">
                <p class="product__name-text">
                    {{ productItem.name }}
                </p>
            </div>
            <div v-if="productItem.isAvailable" class="product__price">
                <p class="product__price-text">
                    {{ formattedPrice }} ₽
                </p>
                <p v-if="isProductOnDiscount" class="product__price-text product__price-text_old">
                    {{ formattedOldPrice }} ₽
                </p>
            </div>
        </div>
        <div class="product__footer">
            <button v-if="productItem.isAvailable" class="btn">
                Купить
            </button>
            <button v-else class="btn btn_full-width btn_grey">
                Сообщить о поступлении
            </button>
        </div>
    </div>
</template>