<template>
    <input :class="$style.ui_input" :disabled="props.isDisabled" :placeholder="props.placeholder" :value="props.modelValue" @input="onInput">
</input>
</template>


<script setup lang="ts">
    interface IProps {
        isDisabled?: boolean;
        placeholder?: string;
        modelValue?: string;
    }
    interface IEmit {
        (e: 'update:modelValue', value: string): void
    }

    const props = defineProps<IProps>()

    const emit = defineEmits<IEmit>()
    const onInput = (e: Event) => {
        const target = e.target as HTMLInputElement
        emit('update:modelValue', target.value)
    }
</script>


<style module lang="scss">
    .ui_input{
        cursor:text;
        background: var(--color-transp);
        border-radius: 10px;
        padding:0 10px;
        height: 50px;
        max-width: 1000px;
        font-size: 100%;
        border: 2px solid var(--color-primary);
        transition: 0.2s;
    }
    .ui_input::placeholder{
        color:var(--color-gray);
    }
    .ui_input:disabled{
        border: 2px solid var(--color-gray-dark);
        cursor:default;
    }
    .ui_input:hover, .ui_input:focus {
        background:var(--color-gray-light);
    }
</style>