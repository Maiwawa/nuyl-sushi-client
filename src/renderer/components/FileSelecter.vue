<template>
    <input type="file" @change="handleFiles">
    <input type="button" value="send" @click="getFile()">
</template>

<script>
export default {
    name: "FileSelecter",
    methods: {
        getFile() {
            alert('function called')
        },
        handleFiles: function (element) {
            let file = element.target.files[0];
            let reader = new FileReader();
            reader.onload = () => {
                this.convert(reader.result);
            };
            reader.readAsText(file);
            alert('function called')
        },
        convert: function (str) {
            //TODO
        }
    }
}


</script>