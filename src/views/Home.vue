<template>
  <main class="w-screen h-screen grid grid-cols-3 place-content-center gap-4">
    <!-- School Title -->
    <section>
      <div>彰化縣梧鳳小學</div>
      <router-link to="/about" class="relative">
        <img
          src="@/assets/images/Story_v2.png"
          class="pointer-events-none select-none"
          alt="Column_1"
        />
        <span
          class="absolute inset-0 flex items-center justify-center ps-5 tracking-widest"
          >校園探索</span
        >
      </router-link>
    </section>
    <section>
      <router-link to="/actions" class="relative"
        ><img
          src="@/assets/images/About_v2.png"
          class="pointer-events-none select-none"
          alt="Column_1"
        />
        <span
          class="absolute inset-0 flex items-center justify-center ps-5 tracking-widest"
          >SDGs行動</span
        ></router-link
      >
    </section>
    <section>
      <router-link to="/sdgs" class="relative"
        ><img
          src="@/assets/images/profile.png"
          class="pointer-events-none select-none"
          alt="Column_1"
        />
        <span
          class="absolute inset-0 flex items-center justify-center ps-5 tracking-widest"
          >SDGs成果</span
        ></router-link
      >
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
