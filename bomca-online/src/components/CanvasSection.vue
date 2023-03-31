<script setup>
import { ref } from 'vue';

const props = defineProps({
    title: String
})

function addItem() {
    if (itemsRef.value[itemsRef.value.length - 1].value === "") {
        itemsRef.value[itemsRef.value.length - 1].value = " "
    }
    items.value[items.value.length - 1] = itemsRef.value[itemsRef.value.length - 1].value
    items.value.push("");
    setTimeout(() => {
        itemsRef.value[itemsRef.value.length - 1].focus();
    }, 2);
}

function deleteItem() {
    if (items.value.length > 1)
    {
        items.value.pop();
        setTimeout(() => {
            itemsRef.value[itemsRef.value.length - 1].focus();
        }, 2);
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
            <input type="text" v-for="item in items" ref="itemsRef" class="bg-transparent outline-none w-full placeholder:italic placeholder:text-black/30 border-l border-slate-800/10 pl-4" placeholder="add an item ... "
                :value="item" @keydown.enter="addItem()" @keydown.delete="deleteItem()" />

        </div>
    </div>
</template>