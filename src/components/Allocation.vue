
<script setup lang="ts">
import { storeToRefs } from 'pinia';
import { useWalletStore } from '@/stores/wallet';
import numeral from 'numeral'
import { useGlobalStore } from '@/stores/global';
import { computed, Ref, ref } from '@vue/reactivity';
const { getUsedDelegations, getTotalStaked } = storeToRefs(useWalletStore())
const { theme } = storeToRefs(useGlobalStore())

const colors = [
    '#B03173', '#B45285', '#B47796', '#6D0F3E', '#B915EB', '#C53CEE', '#640A7F',
    '#9223F9', '#D1B0F0', '#9B6CC8'
]
let used: Ref<string[]> = ref([])

const sections = computed(() => {
    used.value = []
    const mapped = getUsedDelegations.value.map((delegation) => {
        let stakeValue;
        if (delegation.amount === 0) {
            stakeValue = 0
        } else {
            stakeValue = ((delegation.amount / (10 ** 18)) / parseFloat(getTotalStaked.value)) * 100
        }
        return { label: delegation.validator_info.name, address: delegation.validator_address, value: stakeValue, color: randomColorIndex() }
    })
    return mapped
})
function randomColorIndex() {
    const randomColor = colors.filter((element) => !used.value.includes(element))[Math.floor(Math.random() * colors.length)]
    return randomColor
}
</script>

<template>
    <div class="flex flex-1 flex-col justify-center items-center" v-if="getUsedDelegations.length > 0">
        <div class="flex flex-none">
            <div class="flex flex-none rounded-full p-2 shadow-light-depth dark:shadow-dark-depth ">
                <vc-donut :background="theme === 'dark' ? '#313547' : '#edeff2'" :size="130" unit="px" :thickness="25"
                    :sections="sections" :start-angle="0" :auto-adjust-text-size="true">
                    <span class="text-xs dark:text-white text-black">Allocation</span>
                </vc-donut>
            </div>
        </div>
        <div class="flex flex-none  flex-wrap justify-center items-center">
            <template v-for="section of sections">
                <div class="flex flex-none space-x-2 m-1">
                    <div :style="`background-color:${section.color}`" class="w-6 h-6 rounded-lg"></div>
                    <span>
                        <router-link :to="`/validators/${section.address}`">{{ section.label }}</router-link>
                        ({{ numeral(section.value / 100).format('%0') }})
                    </span>
                </div>
            </template>
        </div>
    </div>
</template>

