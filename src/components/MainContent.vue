<template>
    <header class="bg-white shadow">
        <div class="mx-auto px-5 py-6 sm:px-6 lg:px-8">
            <h1 class="text-2xl font-bold tracking-tight text-gray-900">Image Upload</h1>
        </div>
    </header>
    <main>
        <div class="mx-auto max-w-7xl py-6 sm:px-6 lg:px-8">
            <form id="upload-from" class="p-5" @submit.prevent="submit">
                <avatar-input v-model="form.avatar" :default-src="form.src"></avatar-input>
                <!-- <input type="submit" value="submit"
                    class="border border-indigo-500 bg-indigo-500 text-white rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-indigo-700 focus:outline-none focus:shadow-outline cursor-pointer"> -->
            </form>
            <p v-pre>Result : {{ prediction }}</p>
        </div>
    </main>
</template>
  
<script lang="ts">
import { reactive } from 'vue';
import image from '../assets/placeholder.jpg';
import AvatarInput from './AvatarInput.vue';

export default {
    components: {
        AvatarInput
    },
    setup() {
        const form = reactive({
            avatar: null,
            src: image
        });

        const submit = () => {
            console.log('submit', form);
            // call api
        };

        return {
            form,
            submit
        };
    }
};
</script>
  
<style scoped></style>