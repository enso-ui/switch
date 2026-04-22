<template>
    <label class="vue-switch">
        <label class="control-label"
            @click="toggle">
            <slot name="before"/>
        </label>
        <input class="checkbox"
            type="checkbox"
            :value="modelValue"
            @click.stop
            @keydown.prevent.enter="toggle"
            @keydown.space="toggle"
            :disabled="disabled || readonly"
            :checked="modelValue">
        <label class="control-switch"
            :class="[{ 'checked': modelValue, 'disabled': disabled || readonly }]"
            @click="toggle"/>
        <label class="control-label"
            @click="toggle">
            <slot name="after"/>
        </label>
    </label>
</template>

<script>
export default {
    name: 'VueSwitch',

    props: {
        disabled: {
            type: Boolean,
            default: false,
        },
        readonly: {
            type: Boolean,
            default: false,
        },
        modelValue: {
            type: [Boolean, Number],
            required: true,
            default: false,
        },
    },

    emits: ['update:modelValue'],

    methods: {
        toggle() {
            if (!this.disabled && !this.readonly) {
                this.$emit('update:modelValue', !this.modelValue);
            }
        },
    },
};
</script>

<style lang="scss" src="./styles/switch.scss"></style>
