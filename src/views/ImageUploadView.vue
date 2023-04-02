<script setup lang="ts">
import {ref} from 'vue'

const uploadMessage = ref("")
const image = ref(new FormData())

function setImage(event: any) {
  const formData = new FormData()
  formData.append("file", event.target.files[0])
  image.value = formData
}

function upload() {
  fetch("http://localhost:8080/upload", {
    method: "POST",
    body: image.value
  }).then(response => {
    if (response.ok) {
      setUploadMessage("Image uploaded.")
    } else {
      setUploadMessage("Something went wrong! :(")
    }
  })
}
function setUploadMessage(message: string) {
  uploadMessage.value = message
}

</script>

<template>
  <div class="about">
    <h1>This is the image upload page</h1>
    <input type="file" @change="setImage" accept="image/*">
    <button type="button" @click="upload">Upload</button>
    <h2>{{uploadMessage}}</h2>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
