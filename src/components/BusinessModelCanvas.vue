<script setup>
import CanvasSection from './CanvasSection.vue';
import langData from '../assets/language.json';
import languageIcon from './icons/languageIcon.vue';
import { ref, inject } from 'vue';
import SaveIcon from './icons/saveIcon.vue';
import ClearIcon from './icons/clearIcon.vue';

const _lang = ref(inject("lang"));

// all canvas sections
const keyPartners = ref(null);
const keyActivity = ref(null);
const keyResource = ref(null);
const valueProposition = ref(null);
const customerRel = ref(null);
const channels = ref(null);
const customersSegment = ref(null);
const costStructure = ref(null);
const incomeStrems = ref(null);


function changeLang() {
    localStorage.setItem("lang", ((_lang.value === "fa") ? "en" : "fa"))
    _lang.value = ((_lang.value === "fa") ? "en" : "fa");
    location.reload();
}

function saveData() {
    localStorage.setItem("canvasStructure", JSON.stringify({
        "key-partners": keyPartners.value.items,
        "key-activity": keyActivity.value.items,
        "key-resource": keyResource.value.items,
        "value-propos": valueProposition.value.items,
        "customer-rel": customerRel.value.items,
        "channels": channels.value.items,
        "customers-segment": customersSegment.value.items,
        "cost-structure": costStructure.value.items,
        "income-strems": incomeStrems.value.items
    }))
}

function clearAll() {
    localStorage.setItem("canvasStructure", JSON.stringify({
        "key-partners": [""],
        "key-activity": [""],
        "key-resource": [""],
        "value-propos": [""],
        "customer-rel": [""],
        "channels": [""],
        "customers-segment": [""],
        "cost-structure": [""],
        "income-strems": [""]
    }));
    loadData();
}

function loadData() {
    setTimeout(() => {
        let canvasStructure = localStorage.getItem("canvasStructure")
        if (canvasStructure != undefined & canvasStructure != null & canvasStructure !== "") {
            let loadedData = JSON.parse(canvasStructure);
            keyPartners.value.items = loadedData["key-partners"];
            keyActivity.value.items = loadedData["key-activity"];
            keyResource.value.items = loadedData["key-resource"];
            valueProposition.value.items = loadedData["value-propos"];
            customerRel.value.items = loadedData["customer-rel"];
            channels.value.items = loadedData["channels"];
            customersSegment.value.items = loadedData["customers-segment"];
            costStructure.value.items = loadedData["cost-structure"];
            incomeStrems.value.items = loadedData["income-strems"];
        }
        else {
            keyPartners.value.items = [""]
            keyActivity.value.items = [""]
            keyResource.value.items = [""]
            valueProposition.value.items = [""]
            customerRel.value.items = [""]
            channels.value.items = [""]
            customersSegment.value.items = [""]
            costStructure.value.items = [""]
            incomeStrems.value.items = [""]
        }
    }, 2);
}

loadData();
</script>

<template>
    <div class="flex flex-col items-stetch justify-start w-full h-full p-2">
        <!-- Bussiness Model Title -->
        <div class="bg-black/10 shadow rounded-lg py-3 px-5 gap-3 flex justify-between items-center mb-3">
            <div class="flex flex-col justify-center items-start w-full gap-0">
                <input type="text"
                    class=" text-lg bg-transparent border-none outline-none font-medium text-gray-900 w-full placeholder:italic placeholder:text-black/50"
                    :placeholder="langData[_lang]['title-placeholder']">
                <input type="text"
                    class=" text-base bg-transparent border-none outline-none font-medium text-gray-700 italic w-full placeholder:italic placeholder:text-black/40"
                    :placeholder="langData[_lang]['sub-title-placeholder']">
            </div>
            <button
                class="flex items-center justify-center gap-1 bg-gradient-to-t from-gray-500/40 to-white/10 px-2 h-11 flex-none text-gray-800 rounded-md hover:bg-gray-500/40 transition-colors duration-200 shadow-md shadow-slate-950/30 border border-gray-500/20"
                type="button" @click="clearAll()">
                <ClearIcon class="opacity-75" />
            </button>
            <button
                class="flex items-center justify-center gap-1 bg-gradient-to-t from-gray-500/40 to-white/10 px-2 h-11 flex-none text-gray-800 rounded-md hover:bg-gray-500/40 transition-colors duration-200 shadow-md shadow-slate-950/30 border border-gray-500/20"
                type="button" @click="saveData()">
                <SaveIcon class="opacity-75" />
            </button>
            <button
                class="flex items-center justify-center gap-1 bg-gradient-to-t from-gray-500/40 to-white/10 px-4 h-11 flex-none text-gray-800 rounded-md hover:bg-gray-500/40 transition-colors duration-200 shadow-md shadow-slate-950/30 border border-gray-500/20"
                type="button" @click="changeLang()">
                <languageIcon />
                <p v-if="_lang === 'fa'" class="text-sm opacity-80 font-source">EN</p>
                <p v-else class="text-sm pt-1 opacity-80 font-vazir">فا</p>
            </button>
        </div>
        <!-- Canvas Consept -->
        <div class="flex flex-col justify-start items-start w-full h-full gap-3">
            <div
                :class="`flex ${(_lang === 'fa') ? 'flex-row-reverse' : 'flex-row'} items-stretch justify-center w-full h-full gap-3`">
                <CanvasSection ref="keyPartners" :title="langData[_lang]['section-ky-part']" />
                <div class="flex flex-col items-stretch justify-start w-full h-full gap-3">
                    <CanvasSection ref="keyActivity" :title="langData[_lang]['section-ky-act']" />
                    <CanvasSection ref="keyResource" :title="langData[_lang]['section-ky-res']" />
                </div>
                <CanvasSection ref="valueProposition" :title="langData[_lang]['section-val']" />
                <div class="flex flex-col items-stretch justify-start w-full h-full gap-3">
                    <CanvasSection ref="customerRel" :title="langData[_lang]['section-cous-rel']" />
                    <CanvasSection ref="channels" :title="langData[_lang]['section-chnl']" />
                </div>
                <CanvasSection ref="customersSegment" :title="langData[_lang]['section-cus-seg']" />
            </div>
            <div
                :class="`flex ${(_lang === 'fa') ? 'flex-row-reverse' : 'flex-row'} items-stretch justify-center gap-3 w-full h-72`">
                <CanvasSection ref="costStructure" :title="langData[_lang]['section-cst-stru']" />
                <CanvasSection ref="incomeStrems" :title="langData[_lang]['section-incm-strm']" />
            </div>
        </div>
    </div>
</template>