<template>
<div class="parent card">
    <h2>Parent component</h2>
    <pre>{{form}}</pre>
    <app-child
        v-model:form="form"
        :options="options"
    />
</div>
</template>

<script lang="ts" setup>
// Оставил всё внутри компонента для простоты чтения, но обычно разбиваю на default/use-parent/index/types/vue компонент,
// ну и папкам model и ui по FSD
import AppChild from "@/components/child/app-child.vue"
import {ref} from "vue";


export interface FormI {
    input: string,
    select: OptionI
}
export interface OptionI {
    id: number,
    value: string
}

const form = ref<FormI>({
    input: 'in1234112',
    select: {
        id: 1,
        value: 'test1'
    }
})

const options: OptionI[] = [
    {
        id: 1,
        value: 'test1'
    },
    {
        id: 2,
        value: 'test2'
    },
    {
        id: 3,
        value: 'test3'
    },
]
</script>

<style lang="scss">
.card {
    border: 1px solid #212121;
    padding: 20px;
}
</style>