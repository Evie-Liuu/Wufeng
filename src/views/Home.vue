<template>
  <main class="w-screen h-screen grid grid-cols-3 place-content-center gap-4">
    <!-- School Title -->
    <section>
      <div>彰化縣梧鳳小學</div>
      <router-link to="/about" class="relative image-container">
        <img
          src="@/assets/images/Story_v2.png"
          class="pointer-events-none select-none scrollable-image"
          alt="Column_1"
        />
        <span
          class="absolute inset-0 flex items-center justify-center ps-5 tracking-widest"
          >校園探索</span
        >
      </router-link>
    </section>
    <section>
      <router-link to="/actions" class="relative image-container"
        ><img
          src="@/assets/images/About_v2.png"
          class="pointer-events-none select-none scrollable-image"
          alt="Column_1"
        />
        <span
          class="absolute inset-0 flex items-center justify-center ps-5 tracking-widest"
          >SDGs行動</span
        ></router-link
      >
    </section>
    <section>
      <router-link to="/sdgs" class="relative image-container"
        ><img
          src="@/assets/images/profile.png"
          class="pointer-events-none select-none scrollable-image"
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
const currentDirection = ref(null);
const isScrolling = ref(false);

const handleMouseEnter = (event, container) => {
  const rect = container.getBoundingClientRect();
  const y = event.clientY - rect.top;
  const percentage = y / rect.height;

  // 定義中間區域範圍 (上下各 30% 為中間區域，總共 60% 的中間區域)
  const centerStart = 0.2; // 20% 開始
  const centerEnd = 0.8; // 80% 結束

  // 如果在中間區域，不進行滑動
  if (percentage >= centerStart && percentage <= centerEnd) {
    return;
  }

  // 根據鼠標進入時的位置決定初始滑動方向
  const newDirection = percentage < 0.5 ? "down" : "up";

  // 如果方向改變，重置動畫
  if (currentDirection.value !== newDirection) {
    currentDirection.value = newDirection;
    container.classList.remove("scroll-up", "scroll-down");
    container.classList.add(`scroll-${newDirection}`);
  }
};

const handleMouseMove = (event, container) => {
  const rect = container.getBoundingClientRect();
  const y = event.clientY - rect.top;
  const percentage = y / rect.height;

  // 定義中間區域範圍 (上下各 30% 為中間區域，總共 60% 的中間區域)
  const centerStart = 0.2; // 20% 開始
  const centerEnd = 0.8; // 80% 結束

  // 如果在中間區域，不進行滑動
  if (percentage >= centerStart && percentage <= centerEnd) {
    // 如果之前有滑動方向，清除它
    if (currentDirection.value) {
      currentDirection.value = null;
      container.classList.remove("scroll-up", "scroll-down");
    }
    return;
  }

  // 根據當前鼠標位置決定滑動方向
  const newDirection = percentage < 0.5 ? "down" : "up";

  // 如果方向改變，添加一點延遲來避免過於頻繁的切換
  if (currentDirection.value !== newDirection) {
    currentDirection.value = newDirection;

    // 使用 requestAnimationFrame 確保平滑過渡
    requestAnimationFrame(() => {
      container.classList.remove("scroll-up", "scroll-down");
      container.classList.add(`scroll-${newDirection}`);
    });
  }
};

const handleMouseLeave = (container) => {
  // 滑鼠移開時重置圖片位置和狀態
  container.classList.remove("scroll-up", "scroll-down");
  currentDirection.value = null;
  isScrolling.value = false;
};

onMounted(() => {
  setTimeout(() => {
    isLoaded.value = true;
  }, 100);

  // 為每個圖片容器添加事件監聽器
  const containers = document.querySelectorAll(".image-container");
  containers.forEach((container) => {
    container.addEventListener("mouseenter", (e) =>
      handleMouseEnter(e, container)
    );
    container.addEventListener("mousemove", (e) =>
      handleMouseMove(e, container)
    );
    container.addEventListener("mouseleave", () => handleMouseLeave(container));
  });
});
</script>
<style scoped>
.image-container {
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s ease;
  height: 300px; /* 根據需要調整高度 */
}

.image-container:hover {
  transform: scale(1.05);
}

.scrollable-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  transform: translateY(0);
}

/* 滑動狀態類 */
.image-container.scroll-down .scrollable-image {
  transform: translateY(20%);
}

.image-container.scroll-up .scrollable-image {
  transform: translateY(-20%);
}

/* 響應式設計 */
@media (max-width: 768px) {
  .image-container {
    height: 200px;
  }

  .image-container.scroll-down .scrollable-image {
    transform: translateY(15%);
  }

  .image-container.scroll-up .scrollable-image {
    transform: translateY(-15%);
  }
}
</style>
