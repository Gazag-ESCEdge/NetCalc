<template>
    <div class="verticalCenter">
    <div class="calcApp">
        <h1>Калькулятор подсетей</h1>

        <UiField label="Введите IP-адрес">
            <UiInput placeholder="Пример: 192.168.0.1" v-model="ip"/>
        </UiField>

        <UiField label="Выберите маску сети">
            <UiSelect v-model="selectedMask" :options="masksOption"></UiSelect>
        </UiField>

        <UiButton :isDisabled="!ipValid" @click="calculate">Рассчитать</UiButton>
        
        <div v-if="selectedMask && result.adr" class="resultDiv">
            <span><b>IP-адрес: </b>{{ result.ip }}</span>
            <span><b>Маска: </b>{{ result.mask }}</span>
            <span><b>Адрес сети: </b>{{ result.adr }}</span>
            <span><b>Количество возможных адресов: </b>{{ result.count }}</span>
        </div>
    </div>
    </div>
</template>

<script setup lang="ts">
    import { masksOption } from '../constants/masksOption';
    import { isIpValid } from '../functions/isIpValid';
    import { getNetworkAdress } from '../functions/getNetworkAdress';
    import { getAddressesCount } from '../functions/getAddressesCount';
    import { ref, computed } from "vue";
    import UiInput from './UiInput.vue';
    import UiField from './UiField.vue';
    import UiButton from './UiButton.vue';
    import UiSelect from './UiSelect.vue';
    
    const ip = ref("");
    const selectedMask = ref(masksOption[0]);
    const result = ref({
        ip: "",
        mask: "",
        adr: "",
        count: 0
    });

    const ipValid = computed(()=>isIpValid(ip.value))

    function calculate(){
        result.value.ip=ip.value
        result.value.mask=selectedMask.value
        result.value.adr=getNetworkAdress(ip.value,selectedMask.value)
        result.value.count=getAddressesCount(selectedMask.value)
    }
</script>