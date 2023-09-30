<script>
import {defineComponent} from 'vue'
import Check from "./icons/Check.vue";

export default defineComponent({
    name: "VCheckbox",
    components: {Check},
    emits: ['update:checked'],
    props: {
        checked: {
            type: Boolean,
            required: true,
        },
        checkbox: {
            type: Object,
            required: true,
        },
    },
    methods: {
        toggleCheck () {
            this.$emit('update:checked', !this.checked)
        }
    }

})
</script>

<template>
    <div
        @click="toggleCheck"
        :class="{
            'checkbox_active': checked,
        }"
        class="checkbox"
    >
        <div class="checkbox__inner">
            <Check v-if="checked" class="checkbox__check" />
        </div>
        <p class="checkbox__label">
            {{ checkbox.label }}
        </p>
    </div>
</template>