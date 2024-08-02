<template>
  <q-page>
    <div class="row q-col-gutter-md">
      <div class="col-12">
        <h6>Geolocation example</h6>
        GPS position: <strong>{{ position }}</strong>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { Geolocation } from '@capacitor/geolocation';
import { ref, onMounted } from 'vue';

const position = ref('determining...');

function getCurrentPosition() {
  Geolocation.getCurrentPosition().then((newPosition) => {
    console.log('Current', newPosition);
    position.value = newPosition;
  });
}

let geoId;

onMounted(() => {
  getCurrentPosition();

  // we start listening
  geoId = Geolocation.watchPosition({}, (newPosition) => {
    console.log('New GPS position');
    position.value = newPosition;
  });
});

</script>
