<script>
import {defineComponent} from 'vue'
import Divider from "./icons/Divider.vue";
import VInput from "./VInput.vue";

export default defineComponent({
    name: "VPriceRange",
    components: {
        VInput,
        Divider,
    },
    data: function () {
        return {
            price: {
                from: '0',
                to: '9999',
            },
        }
    },
    watch: {
        price: {
            deep: true,
            handler(newVal) {
                let [from, to] = [Number(newVal.from), Number(newVal.to)];
                if (from > to) {
                    this.price.from = '0';
                    this.price.to = '9999';
                }
            },
        },
    },
})
</script>

<template>
    <div class="price-range">
        <div class="price-range__input-wrap">
            <VInput :is-price="true" v-model="price.from" :placeholder="'0'">
                <p class="input__prefix-text">
                    от
                </p>
            </VInput>
        </div>
        <div class="price-range__divider">
            <Divider />
        </div>
        <div class="price-range__input-wrap">
            <VInput :is-price="true" v-model="price.to" :placeholder="'9999'">
                <p class="input__prefix-text">
                    до
                </p>
            </VInput>
        </div>
    </div>
</template>