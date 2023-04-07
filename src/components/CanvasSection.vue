<script setup>
import { ref, inject } from 'vue';

const _lang = ref(inject("lang"));


const props = defineProps({
    title: String
})

function insertAt(array, index, ...elementsArray) {
    array.splice(index, 0, ...elementsArray);
}

function addItem(event) {
    items.value[event.target.id] = event.target.value
    insertAt(items.value, parseInt(event.target.id) + 1, "");
    setTimeout(() => {
        itemsRef.value[parseInt(event.target.id) + 1].focus();
    }, 0.01);
}

function editItem(event) {
    items.value[event.target.id] = event.target.value
}

function deleteItem(event) {
    if (event.target.value.length === 0) {
        if (items.value.length > 1) {
            items.value.splice(event.target.id, 1);
            setTimeout(() => {
                try {
                    itemsRef.value[event.target.id - 1].focus();
                } catch (error) {

                }
            }, 0.01);
        }
    }
}


function hendelClickOnField() {
    setTimeout(() => {
        itemsRef.value[itemsRef.value.length - 1].focus();
    }, 1);
}

const items = ref([""]);

const itemsRef = ref([]);

defineExpose({
    items
})

</script>

<template>
    <section class="bg-black/10 shadow rounded-lg w-full h-full flex flex-col justify-start items-center">
        <div class="w-full py-2 px-4 flex justify-between items-center gap-2 bg-gradient-to-t from-black/10 to-white/[0.03] rounded-t-md shadow"
            @click="($event) => { }">
            <p class="text-gray-800">{{ props.title }}</p>
        </div>
        <div :class="`w-full pt-2 ${(_lang === 'fa') ? 'pr-4' : 'pl-4'} text-gray-700`">
            <input autocapitalize="off" autocomplete="off" type="text" v-for="item in items" ref="itemsRef" :id="items.indexOf(item)"
                :class="`bg-transparent outline-none w-full ${(_lang === 'fa') ? 'border-r pr-4' : 'border-l pl-4'} border-slate-800/10`"
                :value="item" @keydown.enter="addItem($event)" @change="editItem($event)"
                @keydown.delete="deleteItem($event)" />
        </div>
        <div class="flex-1 flex w-full h-full cursor-text" @click="hendelClickOnField()"></div>
    </section>
</template>