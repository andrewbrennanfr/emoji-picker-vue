<script lang="ts">
import Input from "@/components/Input.vue";
import Wysiwyg from "@/components/Wysiwyg.vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
    components: {
        Input,
        Wysiwyg,
    },
    setup() {
        const input = ref("");
        const wysiwyg = ref<any | null>(null);

        return {
            handleChangeInput(event: Event) {
                input.value = (event.target as HTMLInputElement).value;
            },
            handleChangeWysiwyg(event: Event) {
                const element = document.createElement("div");
                element.innerHTML = (event.target as HTMLDivElement).innerHTML;

                const imgs = element.querySelectorAll("img");

                imgs.forEach((img) => {
                    const text = document.createTextNode(
                        img.getAttribute("alt") || ""
                    );

                    element.replaceChild(text, img);
                });

                input.value = element.innerText;
            },
            input,
            wysiwyg,
        };
    },
});
</script>

<template>
    <div>
        <Input :onChange="handleChangeInput" :value="input" />
        <Wysiwyg :onChange="handleChangeWysiwyg" :value="input" ref="wysiwyg" />
    </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@300&display=swap");

* {
    appearance: none;
    background: none;
    border: none;
    box-sizing: border-box;
    color: inherit;
    font: inherit;
    list-style: none;
    margin: 0;
    outline: none;
    padding: 0;
    text-decoration: none;
}

body {
    font: 400 1.6rem/1.8 "Nunito Sans", sans-serif;
}

body,
html {
    height: 100%;
    width: 100%;
}

html {
    font: normal 0.625em/1 -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
        "Segoe UI Symbol";
}

main {
    display: block;
    min-height: 100%;
    padding: 10px;
    width: 100%;
}
</style>
