<template>
    <select :value="props.modelValue" :disabled="props.isDisabled" :class="$style.ui_select" @change="onChange">
        <option v-for="opt in props.options" :key="opt" :value="opt">
            {{ opt }}
        </option>
    </select>
</template>
    
    
<script setup lang="ts">
    interface IProps {
        modelValue?: string
        isDisabled?: boolean
        options?: any[]
    }
    interface IEmit {
        (e: 'update:modelValue', value: string): void
    }
    
    const props = defineProps<IProps>()
    const emit = defineEmits<IEmit>()
    
    const onChange = (e: Event) => {
        const target = e.target as HTMLSelectElement
        emit('update:modelValue', target.value)
    }
</script>


<style module lang="scss">
    .ui_select{
        background: var(--color-transp);
        border-radius: 10px;
        padding:0 10px;
        height: 50px;
        max-width: 1000px;
        font-size: 100%;
        border: 2px solid var(--color-primary);
        transition: 0.2s;
    }
    .ui_select:disabled{
        border: 2px solid var(--color-gray-dark);
    }
    .ui_select:hover, .ui_select:focus {
        background:var(--color-gray-light);
    }
</style>