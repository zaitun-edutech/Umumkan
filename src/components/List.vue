<template>
  <li>{{ row.merk }} | {{ row.tahun }} | {{ row.harga }} |</li>
  <li><a :href="row.down">download</a></li>
</template>

<script setup>
// export default {
//   props: {
//     row: Object,
//   },
// };
defineProps({
  row: Object,
});
</script>

<style></style>
