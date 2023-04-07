<script setup>
import BusinessModelCanvas from '../components/BusinessModelCanvas.vue';
import { provide, ref } from 'vue';

let storredLang = localStorage.getItem("lang")
console.log(storredLang);
if (storredLang == undefined || storredLang == null || storredLang === "") {
  localStorage.setItem("lang", "en");
}
const lang = ref(storredLang);

provide("lang", lang.value);
</script>

<template>
  <div
    :class="`h-full overflow-x-hidden bg-gradient-to-tr from-white/50 via-white/40 to-white/60 backdrop-blur-3xl shadow-white/20 shadow-xl w-full mx-auto rounded-xl relative z-10 ${(lang === 'fa') ? 'font-vazir' : 'font-source'}`">
    <BusinessModelCanvas />
  </div>
</template>
