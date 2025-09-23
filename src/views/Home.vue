<template>
  <main
    class="relative w-screen h-screen grid grid-cols-3 place-content-center gap-4 bg-[url('@/assets/images/Mobile/Plants_Mobile.png'),url('@/assets/images/Mobile/mobile_Bcakground_1.png')] [background-size:cover,cover] overflow-hidden lg:bg-[url('@/assets/images/Background.png')] lg:bg-cover lg:bg-center"
  >
    <!-- School Title -->
    <section>
      <router-link to="/about" class="image-container gap-3">
        <div class="flex flex-col items-center">
          <img
            src="@/assets/images/Campus_Exploration.png"
            class="pointer-events-none select-none scrollable-image mb-2"
            alt="Column_1"
          />
        </div>
        <div class="flex flex-col items-center">
          <img
            src="@/assets/images/School_Name.png"
            class="pointer-events-none select-none scrollable-image"
            alt="Column_1"
          />
        </div>
      </router-link>
    </section>
    <section>
      <router-link to="/actions" class="image-container gap-3">
        <div class="flex flex-col items-center w-95">
          <img
            src="@/assets/images/scene.webp"
            class="pointer-events-none select-none scrollable-image"
            alt="Column_1"
          />
        </div>
        <div class="flex flex-col items-center">
          <img
            src="@/assets/images/SDGs_Green_Actions.png"
            class="pointer-events-none select-none scrollable-image"
            alt="Column_1"
          />
        </div>
        <div class="flex flex-col items-center w-95">
          <img
            src="@/assets/images/scene2.webp"
            class="pointer-events-none select-none scrollable-image"
            alt="Column_1"
          />
        </div>
      </router-link>
    </section>
    <section>
      <router-link to="/sdgs" class="image-container gap-3">
        <div class="flex flex-col items-center">
          <img
            src="@/assets/images/SDGs_Result.png"
            class="pointer-events-none select-none scrollable-image mb-2"
            alt="Column_1"
          />
        </div>
        <div class="flex flex-col items-center">
          <img
            src="@/assets/images/Trans.png"
            class="pointer-events-none select-none scrollable-image"
            alt="Column_1"
          />
        </div>
      </router-link>
    </section>

    <img
      src="@/assets/images/Plants_Web.webp"
      alt="Plants_Web"
      class="hidden lg:block absolute top-0 left-0 w-full object-cover z-20 pointer-events-none"
    />
    <img
      src="@/assets/images/WuFeng_Logo.webp"
      alt="Plants_Web"
      class="hidden lg:block absolute bottom-5 right-5 w-20 object-cover z-20 pointer-events-none"
    />
  </main>
</template>
<script setup>
import { ref, onMounted } from "vue";

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
  const centerStart = 0.4; // 40% 開始
  const centerEnd = 0.6; // 60% 結束

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
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.image-container:hover {
  transform: scale(1.05);
}

.scrollable-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 2s cubic-bezier(0.4, 0, 0.2, 1);
  transform: translateY(0);
}

/* 滑動狀態類 */
.image-container.scroll-down .scrollable-image {
  transform: translateY(30%);
}

.image-container.scroll-up .scrollable-image {
  transform: translateY(-30%);
}

/* 中間三張圖片統一移動幅度 - 使用固定像素值確保一致性 */
section:nth-child(2) .image-container.scroll-down .scrollable-image {
  transform: translateY(350px);
}

section:nth-child(2) .image-container.scroll-up .scrollable-image {
  transform: translateY(-200px);
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

  /* 移動端中間三張圖片統一移動幅度 */
  section:nth-child(2) .image-container.scroll-down .scrollable-image {
    transform: translateY(20px);
  }

  section:nth-child(2) .image-container.scroll-up .scrollable-image {
    transform: translateY(-20px);
  }
}
</style>
