<script>
import {defineComponent} from 'vue'
import CrossCircle from "./icons/CrossCircle.vue";

export default defineComponent({
    name: "VInput",
    components: {CrossCircle},
    emits: ['update:model-value'],
    props: {
        modelValue: {
            type: String,
            required: true,
        },
        isPrice: {
            type: Boolean,
            default: false,
        },
        isSearch: {
            type: Boolean,
            default: false,
        },
        placeholder: {
            type: String,
            default: '',
        }
    },
    data: function () {
        return {
            isInFocus: false,
        }
    },
    methods: {
        onInput (e) {
            if (this.isPrice) {
                e.target.value = e.target.value.replace(/[\s\D]/, '');
            }

            this.$emit('update:model-value', e.target.value);
        },

        setIsInFocus(payload) {
            this.isInFocus = payload;
        },

        clearQuery() {
            this.$emit('update:model-value', '');
        },

    },
})
</script>

<template>
    <label
        class="input"
        :class="{
            'input_focused': isInFocus,
        }"
    >
        <div class="input__prefix">
            <slot></slot>
        </div>
        <input
            :value="modelValue"
            :placeholder="placeholder"
            @input="onInput"
            @focus="setIsInFocus(true)"
            @focusout="setIsInFocus(false)"
            :ref="'input'"
            type="text"
            class="input__el"
        >
        <Transition>
            <div v-if="isInFocus && isSearch" class="input__clear-wrap">
                <CrossCircle class="input__clear-img" @click="clearQuery"/>
            </div>
        </Transition>
    </label>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
    transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>