<script setup>
import CanvasSection from './CanvasSection.vue';

</script>

<template>
    <div class="flex flex-col items-stretch justify-start w-full h-full p-2">
        <!-- Bussiness Model Title -->
        <div class="bg-black/10 shadow rounded-lg py-3 px-5 flex justify-between items-center mb-3">
            <div class="flex flex-col justify-center items-start w-full gap-0">
                <input type="text"
                    class=" text-lg bg-transparent border-none outline-none font-medium text-gray-900 w-full placeholder:italic placeholder:text-black/50"
                    placeholder="Title of your Business model">
                <input type="text"
                    class=" text-base bg-transparent border-none outline-none font-medium text-gray-700 italic w-full placeholder:italic placeholder:text-black/40"
                    placeholder="Write down who or what people created this business model canvas">
            </div>
        </div>
        <!-- Canvas Consept -->
        <div class="flex flex-col justify-start items-start w-full h-full gap-3">
            <div class="flex items-stretch justify-center w-full h-full gap-3">
                <CanvasSection title="Key Partners" />
                <div class="flex flex-col items-stretch justify-start w-full h-full gap-3">
                    <CanvasSection title="Key Activity" />
                    <CanvasSection title="Key Resources" />
                </div>
                <CanvasSection title="Value proposition" />
                <div class="flex flex-col items-stretch justify-start w-full h-full gap-3">
                    <CanvasSection title="Customer Relationships" />
                    <CanvasSection title="Channels" />
                </div>
                <CanvasSection title="Customer Segments" />
            </div>
            <div class="flex items-stretch justify-center gap-3 w-full h-72">
                <CanvasSection title="Cost Structure" />
                <CanvasSection title="Income streams" />
            </div>
        </div>
    </div>
</template>