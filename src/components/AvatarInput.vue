<template>
    <div>
        <input type="file" accept="image/*" class="hidden" ref="fileInput" @change="onFileChange">
        <div class="relative inline-block">
            <img :src="src" alt="pet image" class="h-48 w-48 rounded-md object-cover">
            <div class="absolute top-0 h-full w-full bg-black rounded-md bg-opacity-25 flex items-center justify-center">
                <button type="button" @click="browse()"
                    class="rounded-md hover:bg-white hover:bg-opacity-25 p-2 focus:outline-none text-white transition duration-200 font-semibold text-lg">
                    <span>選擇圖片</span>
                </button>
            </div>
        </div>
    </div>
</template>
  
<script lang="ts">
import { ref } from "vue";

export default {
    props: {
        value: File,
        defaultSrc: String
    },
    emits: ['input'],
    setup(props, ctx) {
        const src = ref(props.defaultSrc)
        const fileInput = ref<HTMLInputElement | null>(null);
        const browse = () => {
            fileInput.value?.click();
        }
        const onFileChange = (e: any) => {
            ctx.emit('input', e.target.files[0])
            let reader = new FileReader()
            reader.readAsDataURL(e.target.files[0])
            reader.onload = (e: any) => {
                src.value = e.target?.result
            }
        }

        return {
            src,
            fileInput,
            browse,
            onFileChange
        }
    },
};
</script>

<style></style>