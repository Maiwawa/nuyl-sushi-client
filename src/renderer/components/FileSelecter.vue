<template>
  <input type="file" @change="onFileSelect" accept="video/.mp4" />
  <input type="button" value="send" @click="onUpload()" />
  <video controls width="640" height="360" id="videoPlayer">
    <source src="" type="video/mp4" />
  </video>
</template>

<script>
import axios from "axios";
export default {
  name: "FileSelecter",
  data() {
    return {
      file: "",
    };
  },
  methods: {
    onUpload() {
      let formData = new FormData();
      formData.append("file", this.file);

      axios
        .post("http://localhost:8000/upload/", formData, {
          headers: {
            "Content-Type": "multipart/form-data",
          },
          responseType: "blob",
        })
        .then(function (res) {
          const videoUrl = URL.createObjectURL(res.data);
          const videoPlayer = document.getElementById("videoPlayer");
          videoPlayer.src = videoUrl;
          alert("SUCCESS!!");
        })
        .catch(function (err) {
          alert("FAILURE!!");
          console.log(err);
        });
    },
    onFileSelect(e) {
      this.file = e.target.files[0];
      console.log(this.file);
    },
  },
};
</script>
