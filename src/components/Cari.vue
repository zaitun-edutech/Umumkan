<template>
  <button @click="downloadPdf">download</button>

  <div id="iip">
    <input
      type="text"
      placeholder="cari berdasrkan merk"
      v-model="cari"
      @focus="carikan"
    />
    <button @click="carilah">Cari</button>
    <span v-if="isCari">
      <ul v-for="row in cariKendaraan1" :key="row">
        <List :row="row" />
      </ul>
    </span>
    <span v-if="tidak">
      <h2>Data tidak ditemukan</h2>
    </span>
  </div>
</template>

<script setup>
import jpdf from "jspdf";
import { reactive, ref } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
import List from "./List.vue";

const cari = ref("");
const isCari = ref(false);
const tidak = ref(false);
const kendaraan = reactive([
  {
    merk: "honda",
    tahun: "2018",
    harga: 2000000,
    down: "https://drive.google.com/file/d/1Ug0QyC9RiJKJyr5oVWeD_Ca1FO2Pxw--/view?usp=drivesdk",
  },
  {
    merk: "yamaha",
    tahun: "2019",
    harga: 1500000,
    down: "https://drive.google.com/file/d/1Ug0QyC9RiJKJyr5oVWeD_Ca1FO2Pxw--/view?usp=drivesdk",
  },
  {
    merk: "suzuki",
    tahun: "2020",
    harga: 2000000,
    down: "https://drive.google.com/file/d/1Ug0QyC9RiJKJyr5oVWeD_Ca1FO2Pxw--/view?usp=drivesdk",
  },
]);

const cariKendaraan1 = computed(() => {
  return kendaraan.filter((kendaraan) => {
    if (cari.value === kendaraan.merk) {
      return kendaraan.merk.match(cari.value);
    } else {
      tidak.value = true;
    }
  });
});
const carilah = () => {
  if (cari.value.length > 0 && cariKendaraan1.value.length == 1) {
    isCari.value = true;
    tidak.value = false;
  } else {
    console.log(cariKendaraan1.value.length);
    tidak.value = true;
  }
};
const carikan = () => {
  tidak.value = false;
  isCari.value = false;
};

const cariKendaraan = () => {
  return kendaraan.filter((knd) => {
    return knd.merk.toLowerCase().match(cari.value.toLowerCase());
  });
};
const downloadPdf = () => {
  const doc = new jpdf("p", "pt", "a4");
  doc.html(document.querySelector("#on"), {
    callback: function (pdf) {
      pdf.save("test.pdf");
    },
  });
};
console.log(kendaraan.length);
const buildPdf = () => {};
</script>

<style></style>
