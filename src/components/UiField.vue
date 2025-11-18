<template>
    <label :class="$style.ui_field">
        <span>{{ props.label }}</span>
        <slot></slot>
    </label>
</input>
</template>


<script setup lang="ts">
    interface IProps {
        label?: string;
    }

    const props = defineProps<IProps>()
</script>


<style module lang="scss">
    .ui_field{
        display: flex;
        flex-direction: column;
    }
    .ui_field span {
        font-size:small;
    }
</style>