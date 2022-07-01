<template>
    Type your plain text:<br />
    <input class="input" :value="value" @input="onChange" type="text" />
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
    props: {
        onChange: {
            required: true,
            type: Function as PropType<(event: Event) => void>,
        },
        value: {
            required: true,
            type: String,
        },
    },
});
</script>

<style>
.input {
    border: 1px solid red;
    width: 300px;
}
</style>
