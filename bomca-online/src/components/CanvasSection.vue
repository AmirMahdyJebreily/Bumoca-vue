<script setup>
import { ref } from 'vue';

const props = defineProps({
    title: String
})

function insertAt(array, index, ...elementsArray) {
    array.splice(index, 0, ...elementsArray);
}

function addItem(event) {
    if (event.target.value === "") {
        event.target.value = " "
    }
    items.value[event.target.id] = event.target.value
    insertAt(items.value, parseInt(event.target.id) + 1, "");
    setTimeout(() => {
        itemsRef.value[parseInt(event.target.id) + 1].focus();
    }, 2);
}

function editItem(event) {
    items.value[event.target.id] = event.target.value
}

function deleteItem(event) {
    if (event.target.value.length === 0) {
        if (items.value.length > 1) {
            items.value.splice(event.target.id, 1);
            setTimeout(() => {
                itemsRef.value[event.target.id - 1].focus();
            }, 1);
        }
    }
}

const items = ref([""]);

const itemsRef = ref([]);

</script>

<template>
    <div class="bg-black/10 shadow rounded-lg w-full h-full flex flex-col justify-start items-center">
        <div
            class="w-full py-2 px-4 flex justify-between items-center gap-2 bg-gradient-to-t from-black/5 to-white/[0.04] rounded-t-md shadow">
            <p class="text-gray-800">{{ props.title }}</p>
        </div>
        <div class="flex-1 w-full pt-2 pl-4 text-gray-700">
            <input type="text" v-for="item in items" ref="itemsRef" :id="items.indexOf(item)"
                class="bg-transparent outline-none w-full border-l border-slate-800/10 pl-4" :value="item"
                @keydown.enter="addItem($event)" @change="editItem($event)" @keydown.delete="deleteItem($event)" />

        </div>
    </div>
</template>