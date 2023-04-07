<script setup>
import CanvasSection from './CanvasSection.vue';
import langData from '../assets/language.json';
import { ref, inject } from 'vue';

const _lang = ref(inject("lang"));

function changeLang() {
    localStorage.setItem("lang", ((_lang.value === "fa") ? "en" : "fa"))
    _lang.value = ((_lang.value === "fa") ? "en" : "fa");
    location.reload();
}

</script>

<template>
    <div class="flex flex-col items-stetch justify-start w-full h-full p-2">
        <!-- Bussiness Model Title -->
        <div class="bg-black/10 shadow rounded-lg py-3 px-5 flex justify-between items-center mb-3">
            <div class="flex flex-col justify-center items-start w-full gap-0">
                <input type="text"
                    class=" text-lg bg-transparent border-none outline-none font-medium text-gray-900 w-full placeholder:italic placeholder:text-black/50"
                    :placeholder="langData[_lang]['title-placeholder']">
                <input type="text"
                    class=" text-base bg-transparent border-none outline-none font-medium text-gray-700 italic w-full placeholder:italic placeholder:text-black/40"
                    :placeholder="langData[_lang]['sub-title-placeholder']">
            </div>
            <button
                :class="`bg-gradient-to-t from-gray-500/40 to-white/10 w-11 h-10 pt-0.5 flex-none text-gray-800 rounded-md hover:bg-gray-500/40 transition-colors duration-150 shadow-md shadow-slate-950/30 border border-gray-500/20 ${(_lang === 'fa') ? 'font-sourceW' : 'font-vazir'}`"
                type="button" @click="changeLang()">
                {{ ((_lang === "fa") ? "EN" : "فا") }}
            </button>
        </div>
        <!-- Canvas Consept -->
        <div class="flex flex-col justify-start items-start w-full h-full gap-3">
            <div
                :class="`flex ${(_lang === 'fa') ? 'flex-row-reverse' : 'flex-row'} items-stretch justify-center w-full h-full gap-3`">
                <CanvasSection :title="langData[_lang]['section-ky-part']" />
                <div class="flex flex-col items-stretch justify-start w-full h-full gap-3">
                    <CanvasSection :title="langData[_lang]['section-ky-act']" />
                    <CanvasSection :title="langData[_lang]['section-ky-res']" />
                </div>
                <CanvasSection :title="langData[_lang]['section-val']" />
                <div class="flex flex-col items-stretch justify-start w-full h-full gap-3">
                    <CanvasSection :title="langData[_lang]['section-cous-rel']" />
                    <CanvasSection :title="langData[_lang]['section-chnl']" />
                </div>
                <CanvasSection :title="langData[_lang]['section-cus-seg']" />
            </div>
            <div :class="`flex ${(_lang === 'fa') ? 'flex-row-reverse' : 'flex-row'} items-stretch justify-center gap-3 w-full h-72`">
                <CanvasSection :title="langData[_lang]['section-cst-stru']" />
                <CanvasSection :title="langData[_lang]['section-incm-strm']" />
            </div>
        </div>
    </div>
</template>