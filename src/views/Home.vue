<template>
  <main class="h-screen w-screeen flex flex-col items-center justify-center">
    <!-- School Title -->
    <section>
      <div>彰化縣長安小學</div>
    </section>
    <!-- Menu Buttons -->
    <section class="">
      <div
        :class="[
          'transition-all duration-3000 ease-out',
          isLoaded ? 'opacity-100' : 'opacity-0',
        ]"
        class="flex flex-col lg:flex-row pt-8 lg:pt-0 lg:gap-5 items-center justify-center text-xl lg:text-2xl"
      >
        <router-link
          to="/about"
          class="relative"
          @mouseover="hoveredIndex = 0"
          @mouseleave="hoveredIndex = null"
        >
          <img
            :src="hoveredIndex === 0 ? paint1Selected : paint1Unselected"
            class="pointer-events-none select-none w-52 lg:w-auto"
            alt="Paint_1"
          />
          <span
            class="absolute inset-0 flex items-center justify-center text-white ps-5 tracking-widest"
            >校園探索</span
          >
        </router-link>
        <router-link
          to="/actions"
          class="relative"
          @mouseover="hoveredIndex = 1"
          @mouseleave="hoveredIndex = null"
          ><img
            :src="hoveredIndex === 1 ? paint2Selected : paint2Unselected"
            class="pointer-events-none select-none w-52 lg:w-auto"
            alt="Paint_2"
          />
          <span
            class="absolute inset-0 flex items-center justify-center text-white ps-5 tracking-widest"
            >SDGs行動</span
          ></router-link
        >
        <router-link
          to="/sdgs"
          class="relative -translate-x-1/6"
          @mouseover="hoveredIndex = 2"
          @mouseleave="hoveredIndex = null"
          ><img
            :src="hoveredIndex === 2 ? paint3Selected : paint3Unselected"
            class="pointer-events-none select-none w-52 lg:w-auto"
            alt="Paint_3"
          />
          <span
            class="absolute inset-0 flex items-center justify-center text-white ps-5 tracking-widest"
            >SDGs成果</span
          ></router-link
        >
      </div>
    </section>
  </main>
</template>
<script setup>
import { ref, onMounted } from "vue";
// import ChinesePaintingRing from "@/assets/images/ChinesePaintingRing_v2_Hemei_2.webp";
// import ChinesePaintingRing_mobile from "@/assets/images/Mobile_ChinesePaintingRing_v2_Hemei2.png";
import paint1Unselected from "@/assets/images/Paint_1_v2_Unselected.png";
import paint1Selected from "@/assets/images/Paint_1_v2_Selected.png";
import paint2Unselected from "@/assets/images/Paint_2_v2_Unselected.png";
import paint2Selected from "@/assets/images/Paint_2_v2_Selected.png";
import paint3Unselected from "@/assets/images/Paint_3_v2_Unselected.png";
import paint3Selected from "@/assets/images/Paint_3_v2_Selected.png";

const hoveredIndex = ref(null);
const isLoaded = ref(false);

onMounted(() => {
  setTimeout(() => {
    isLoaded.value = true;
  }, 100);
});
</script>
<style scoped>
</style>
