<template>
    <main>
        <div class="flex flex-col sm:flex-row mr-auto max-w-7xl py-6 sm:px-6 lg:px-8">
            <form id="upload-from" class="p-5 flex flex-col" @submit.prevent="submit">
                <avatar-input v-model="form.avatar" :default-src="form.src" @input="onFileUploaded"></avatar-input>
                <input type="submit" value="submit"
                    class="border-2 border-red-500 bg-white text-red-500 rounded-md w-48 px-4 py-2  mt-3 transition duration-500 ease select-none hover:bg-red-600 hover:text-white focus:outline-none focus:shadow-outline cursor-pointer">
            </form>
            <div class="p-5 w-96">
                <table class="table w-full bg-white">
                    <thead>
                        <tr>
                            <th class="font-semibold border px-4 py-2 text-gray-900">Class</th>
                            <th class="font-semibold border px-4 py-2 text-gray-900">Score</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td class="border px-4 py-2">Angry</td>
                            <td class="border px-4 py-2">{{ scores.angry }}</td>
                        </tr>
                        <tr>
                            <td class="border px-4 py-2">Sad</td>
                            <td class="border px-4 py-2">{{ scores.sad }}</td>
                        </tr>
                        <tr>
                            <td class="border px-4 py-2">Happy</td>
                            <td class="border px-4 py-2">{{ scores.happy }}</td>
                        </tr>
                        <tr>
                            <td class="border px-4 py-2">Other</td>
                            <td class="border px-4 py-2">{{ scores.other }}</td>
                        </tr>
                        <tr>
                            <th class="font-semibold border px-4 py-2 text-gray-900 text-left" colSpan="2">
                                <span class="font-semibold">Scored Label:</span>&nbsp;
                                <span>{{ scores.label }}</span>
                            </th>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </main>
</template>
  
<script lang="ts">
import { reactive } from 'vue'
import image from '../assets/placeholder.jpg'
import AvatarInput from './AvatarInput.vue'

export default {
    components: {
        AvatarInput
    },
    setup() {
        const form = reactive({
            avatar: '',
            src: image
        })

        const scores = reactive({
            angry: 0,
            sad: 0,
            happy: 0,
            other: 0,
            category: '',
            label: ''
        })

        const onFileUploaded = (file: File) => {
            console.log('The value changed to: ', file)
            Object.assign(form, { avatar: file })
        }

        const submit = async () => {
            console.log('submit', form)
            console.warn('submit', form.avatar)

            // call api
            const formData = new FormData()
            formData.append('file1', form.avatar);

            try {
                const res = await fetch('./api/run', {
                    method: 'POST',
                    body: formData
                });

                if (!res.ok) {
                    throw new Error('Network response was not ok');
                }

                const data = await res.json();
                console.log(data);

                // handle data
                const result = data.prediction
                scores.angry = result['Scored Probabilities_Angry']
                scores.other = result['Scored Probabilities_Other']
                scores.sad = result['Scored Probabilities_Sad']
                scores.happy = result['Scored Probabilities_happy']
                scores.label = result['Scored Labels']
                // console.log('Scored Labels', result['Scored Labels'])
                // console.log('Scored Probabilities_Angry', result['Scored Probabilities_Angry'])
                // console.log('Scored Probabilities_Other', result['Scored Probabilities_Other'])
                // console.log('Scored Probabilities_Sad', result['Scored Probabilities_Sad'])
                // console.log('Scored Probabilities_happy', result['Scored Probabilities_happy'])

            } catch (error) {
                console.error('Error:', error);
            }

        };

        return {
            scores,
            form,
            submit,
            onFileUploaded
        }
    }
}
</script>
  
<style scoped></style>