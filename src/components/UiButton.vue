<template>
    <button :class="$style.ui_button" :disabled="props.isDisabled" :type="props.type" :data-layout="props.layout">
        <slot></slot>
    </button>
</template>


<script setup lang="ts">
interface IProps {
    layout?: 'primary' | 'secondary';
    type?: 'submit' | 'button';
    isDisabled?: boolean;
}

const props = withDefaults(defineProps<IProps>(), {
    layout: 'primary',
    type: 'button',
});
</script>


<style module lang="scss">
    .ui_button{
        cursor:pointer;
        background: var(--color-primary);
        color:var(--color-white);
        border-radius: 10px;
        height: 50px;
        min-width: 150px;
        font-size: 130%;
        border:none;
        box-shadow:0.5px 2px 4px 0px rgba(255, 255, 255, 0.4) inset;
        transition: 0.1s;
        &[data-layout='secondary'] {
            color: var(--color-primary);
            background-color: var(--color-transp);
            border: 2px solid var(--color-primary);
        }
    }
    .ui_button:hover:not(:disabled){
        background: var(--color-primary);
        box-shadow:0.5px 2px 8px 0px rgba(0, 0, 0, 0.2) inset;
        &[data-layout='secondary'] {
            color: var(--color-white);
            border:none;
        }
    }
    .ui_button:active:not(:disabled){
        background: var(--color-primary-dark);
        color:var(--color-gray);
        box-shadow:none;
    }
    .ui_button:disabled{
        background: var(--color-gray-dark);
        cursor:default;
        &[data-layout='secondary'] {
            color: var(--color-gray-dark);
            background-color: var(--color-transp);
            border: 2px solid var(--color-gray-dark);
        }
    }
</style>