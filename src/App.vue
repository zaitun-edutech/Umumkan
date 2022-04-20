<template>
  <div id="on">
    <div>
      <Cari />
    </div>
    <h1>
      <h1>Hallo</h1>
      {{ count }}
    </h1>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Cari from "./components/Cari.vue";

const count = ref(0);
if (count.value < 10) {
  setInterval(() => {
    count.value++;
  }, 1000);
} else {
  count.value = 0;
}
</script>

<style></style>
