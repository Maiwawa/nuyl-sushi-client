<template>
    <input type="file" @change="onFileSelected">
    <input type="button" value="send" @click="onUpload()">

    <video width="120" height="240" controls>
        <source :src="videoFullPath" type="video/mp4">
        Your browser does not support the video tag.
    </video>
</template>

<script>
import axios from 'axios'
export default {
    name: "FileSelecter",
    data() {
        return {
            file: ''
        }
    },
    methods: {
        onUpload() {
            let formData = new FormData();
            formData.append('file', this.file);

            axios.post('',
                formData,
                {
                    headers: {
                        'Content-Type': 'multipart/form-data'
                    }
                }
            ).then(function () {
                console.log('SUCCESS!!');
            })
                .catch(function () {
                    console.log('FAILURE!!');
                });
        },
        onFileSelected(event) {
            this.file = event.target.files[0];
        },
    }
}


</script>