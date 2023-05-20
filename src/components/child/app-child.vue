<template>
    <div class="child card">
        <h2>Child component</h2>
        <pre>{{props.form}}</pre>

        <input
            type="text"
            :value="form.input"
            @input="updateInput($event.target.value)"
        >

        <select
            :value="form.select.id"
            @change="updateSelect($event.target.value)"
            name="select"
            class="select"
        >
            <option value="">Выберите из списка</option>
            <option
                v-for="option in options"
                :key="option.id"
                :value="option.id"
                @click="updateSelect(option.id)"
            >
                {{option.value}}
            </option>
        </select>
    </div>
</template>

<script lang="ts" setup>
import {PropType} from "vue";
import {FormI, OptionI} from "@/components/parent/app-parent.vue";

const props = defineProps({
    form: {
        type: Object as PropType<FormI>,
        required: true
    },
    options: {
        type: Array as PropType<OptionI[]>,
        required: true
    }
})
const emits = defineEmits(['update:form'])

const updateInput = (val: string) => {
    const _form = Object.assign({}, props.form)
    _form.input = val

    emits('update:form', _form)
}
const updateSelect = (optionId: number) => {
    const _form = Object.assign({}, props.form)
    const option = props.options.find(({id}) => id === Number(optionId))

    if (option) {
        _form.select = option
        emits('update:form', _form)
    }
}
</script>

<style lang="scss">
.select {
    display: block;
    margin-top: 20px;
    width: 185px;
}

</style>