<template>
  <main
    class="bg-[url('@/assets/images/Mobile/mobile_Bcakground_1.png')] bg-cover overflow-hidden lg:bg-[url('@/assets/images/Background.png')] lg:bg-cover lg:bg-center"
  >
    <!-- Mobile -->
    <div
      class="relative lg:hidden w-screen h-screen grid grid-cols-2 place-content-center gap-5 px-4 py-8"
    >
      <section class="w-full max-w-md flex flex-col items-center gap-6">
        <router-link to="/sdgs" class="w-full flex justify-center z-5">
          <img
            src="@/assets/images/SDGs_Result.png"
            class="w-full max-w-sm h-auto object-contain border-4 border-gray-100"
            alt="Column_1_result"
          />
        </router-link>
        <div
          class="flex flex-col items-center w-full mb-34 ms-28 scale-190 -translate-y-8"
        >
          <img
            src="@/assets/images/Mobile/School_Name_Mobile.png"
            class="w-full max-w-sm h-auto pointer-events-none select-none"
            alt="Column_1_schoolName"
          />
        </div>
      </section>
      <section class="w-full max-w-md flex flex-col items-center mt-28">
        <router-link to="/about" class="flex-1 w-full flex justify-center z-5">
          <div class="flex flex-col items-center w-full">
            <img
              src="@/assets/images/Campus_Exploration.png"
              class="w-full max-w-sm h-auto object-contain border-4 border-gray-100"
              alt="Column_2_exploration"
            />
          </div>
        </router-link>
        <router-link
          to="/actions"
          class="flex-1 w-full flex justify-center z-5"
        >
          <div class="flex flex-col items-center w-full">
            <img
              src="@/assets/images/SDGs_Green_Actions.png"
              class="w-full max-w-sm h-auto object-contain border-4 border-gray-100"
              alt="Column_2_actions"
            />
          </div>
        </router-link>
      </section>
      <img
        src="@/assets/images/Mobile/Plants_Mobile.png"
        alt="Plants_Mobile"
        class="absolute top-0 left-0 w-full object-fill z-20 pointer-events-none"
      />
    </div>

    <!-- Web -->
    <div
      class="relative hidden w-screen h-screen lg:grid grid-cols-3 place-content-center"
    >
      <section>
        <div class="image-container gap-5">
          <router-link
            to="/about"
            class="flex flex-col items-center xl:translate-x-[8rem]"
          >
            <img
              src="@/assets/images/Campus_Exploration.png"
              class="pointer-events-none select-none scrollable-image border-10 border-gray-100"
              alt="Column_1_exploration"
            />
          </router-link>
          <div class="flex flex-col items-center">
            <img
              src="@/assets/images/School_Name.png"
              class="pointer-events-none select-none scrollable-image"
              alt="Column_1_schoolName"
            />
          </div>
        </div>
      </section>
      <section>
        <div class="image-container gap-5">
          <div
            class="flex flex-col items-center w-100 h-115 xl:translate-x-[3rem]"
          >
            <img
              src="@/assets/images/scene.webp"
              class="pointer-events-none select-none scrollable-image border-8 border-gray-100"
              alt="Column_1"
            />
          </div>
          <router-link to="/actions" class="flex flex-col items-center">
            <img
              src="@/assets/images/SDGs_Green_Actions.png"
              class="pointer-events-none select-none scrollable-image border-5 border-gray-100"
              alt="Column_1"
            />
          </router-link>
          <div
            class="flex flex-col items-center w-100 h-115 xl:-translate-x-[5rem]"
          >
            <img
              src="@/assets/images/scene2.webp"
              class="pointer-events-none select-none scrollable-image border-8 border-gray-100"
              alt="Column_1"
            />
          </div>
        </div>
      </section>
      <section>
        <div class="image-container gap-20">
          <router-link to="/sdgs" class="flex flex-col items-center">
            <img
              src="@/assets/images/SDGs_Result.png"
              class="pointer-events-none select-none scrollable-image border-10 border-gray-100"
              alt="Column_1"
            />
          </router-link>
          <div class="flex flex-col items-center xl:-translate-x-[7rem]">
            <img
              src="@/assets/images/Trans.png"
              class="pointer-events-none select-none scrollable-image"
              alt="Column_1"
            />
          </div>
        </div>
      </section>

      <img
        src="@/assets/images/Plants_Web.webp"
        alt="Plants_Web"
        class="absolute top-0 left-0 w-full object-cover z-20 pointer-events-none"
      />
      <img
        src="@/assets/images/WuFeng_Logo.webp"
        alt="WuFeng_Logo"
        class="absolute bottom-5 right-5 w-20 object-cover z-20 pointer-events-none"
      />
    </div>
  </main>
</template>
<script setup>
import { ref, onMounted } from "vue";

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
  /* cursor: pointer; */
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

/* 行動版優化 */
@media (max-width: 1023px) {
  /* 行動版圖片容器樣式 */
  .lg\:hidden .scrollable-image {
    max-height: none;
    width: auto;
    max-width: 100%;
  }

  /* 確保行動版圖片不會被裁掉 */
  .lg\:hidden img {
    object-fit: contain !important;
    height: auto !important;
    width: 100% !important;
    /* max-width: 320px; */
  }

  /* 行動版容器間距調整 */
  .lg\:hidden section {
    gap: 1.5rem;
  }

  /* 行動版圖片容器 */
  .lg\:hidden .flex {
    width: 100%;
    justify-content: center;
  }
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
