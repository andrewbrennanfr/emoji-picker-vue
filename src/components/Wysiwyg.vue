<template>
    <div>
        Type your wysiwyg text:<br />
        <div
            v-html="html"
            class="wysiwyg"
            contenteditable="true"
            @input="onChange"
        />
    </div>
</template>

<script lang="ts">
import twemoji from 'twemoji'
import { computed, defineComponent, PropType } from 'vue'

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
    setup(props) {
        return {
            html: computed(() =>
                twemoji.parse(props.value, {
                    folder: 'svg',
                    ext: '.svg',
                })
            ),
        }
    },
})
</script>

<style>
img {
    height: 16px;
}

.wysiwyg {
    border: 1px solid blue;
    width: 300px;
}
</style>
