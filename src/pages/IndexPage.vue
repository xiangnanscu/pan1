<template>
  <div>
    <q-btn color="primary" label="Get Picture" @click="captureImage" />
    <q-btn color="primary" label="calculate" @click="cal" />
    {{cnt}}
    <img :src="imageSrc">
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Camera, CameraResultType } from '@capacitor/camera'
const imageSrc = ref('')
const cnt = ref(0)
function cal() {
  console.log("cal ...")
  cnt.value++
}
async function captureImage() {
  const image = await Camera.getPhoto({
    quality: 90,
    allowEditing: true,
    resultType: CameraResultType.Uri
  })
  console.log("take ...")
  // The result will vary on the value of the resultType option.
  // CameraResultType.Uri - Get the result from image.webPath
  // CameraResultType.Base64 - Get the result from image.base64String
  // CameraResultType.DataUrl - Get the result from image.dataUrl
  imageSrc.value = image.webPath
}
</script>
