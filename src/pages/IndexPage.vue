<template>
  <q-page>
    <div class="row q-col-gutter-md">
      <h6>Camera example</h6>
      <div class="col-12">
        <q-btn color="primary" label="Get Picture" @click="captureImage" />
      </div>
      <div class="col-12" v-if="imageSrc !== ''">
        <q-img :src="imageSrc" alt="test" />
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { Camera, CameraResultType } from '@capacitor/camera';
import { ref } from 'vue';

const imageSrc = ref('');

const captureImage = async () => {
  const image = await Camera.getPhoto({
    quality: 90,
    allowEditing: true,
    resultType: CameraResultType.Uri,
  });

  // The result will vary on the value of the resultType option.
  // CameraResultType.Uri - Get the result from image.webPath
  // CameraResultType.Base64 - Get the result from image.base64String
  // CameraResultType.DataUrl - Get the result from image.dataUrl
  imageSrc.value = image.webPath as string;
};
</script>
