<template>
  <div class="gallery">
    <h1>我们的回忆</h1>
    <div
      v-for="(image, index) in images"
      :key="index"
      class="image-container"
      ref="imageContainers"
    >
      <img
        :src="image"
        :alt="`回忆 ${index + 1}`"
        :class="{
          'image': true,
          [animationClasses[index % 3]]: isImageVisible[index]
        }"
      />
      <div
        v-if="isImageVisible[index]"
        class="love-message"
        :class="{ 'animate': isLoveMessageAnimating[index] }"
        @animationend="handleAnimationEnd(index)"
      >
        {{ loveMessages[index] }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue';
// 引入本地图片
import img1 from '../assets/imgs/01.jpg';
import img2 from '../assets/imgs/02.jpg';
import img3 from '../assets/imgs/03.jpg';
import img4 from '../assets/imgs/04.jpg';
import img5 from '../assets/imgs/05.jpg';
import img6 from '../assets/imgs/06.jpg';
import img7 from '../assets/imgs/07.jpg';
import img8 from '../assets/imgs/08.jpg';
import img9 from '../assets/imgs/09.jpg';
import img10 from '../assets/imgs/10.jpg';
import img11 from '../assets/imgs/11.jpg';
import img12 from '../assets/imgs/12.jpg';

const images = ref([
  img1, img2, img3, img4, img5, img6, img7, img8, img9, img10, img11, img12
]);

// 每张图片对应的情话
const loveMessages = ref([
  '你是我藏在微风中的欢喜。',
  '与你走过的时光，皆是浪漫。',
  '你的笑，是我见过最治愈的风景，一生看不够。',
  '在这纷繁世界，你是我想抓住的永恒，永远爱你。',
  '有你在身旁，平凡日子也熠熠生辉，爱你不止朝夕。',
  '你是我生命乐章里最美的旋律，奏响一生的甜蜜。',
  '时间会流逝，可我对你的爱，如同繁星永不落幕。',
  '与你相拥的瞬间，我找到了全世界最温暖的港湾。',
  '你是我漫漫人生路上惊喜，爱你是我不变的选择。',
  '在爱的地图里，你是我唯一的目的地，永不停歇。',
  '你的存在，让我相信爱情是这世上最美好的奇迹。',
  '未来的每个四季，我都想和你一起走过，爱你到永远。'
]);

// 不同图片的动画类
const animationClasses = ref(['fade-in', 'slide-up', 'zoom-in']);
const isImageVisible = ref(new Array(images.value.length).fill(false));
const isLoveMessageAnimating = ref(new Array(images.value.length).fill(false));
const imageContainers = ref([]);

let observer;

const checkImageVisibility = (entries) => {
  entries.forEach((entry) => {
    const index = imageContainers.value.indexOf(entry.target);
    if (entry.isIntersecting && !isImageVisible.value[index]) {
      setTimeout(() => {
        isImageVisible.value[index] = true;
        isLoveMessageAnimating.value[index] = true;
      }, 1000);
    }
  });
};

const handleAnimationEnd = (index) => {
  // 动画结束后重置动画状态
  isLoveMessageAnimating.value[index] = false;
  // 在下一个 DOM 更新周期重新触发动画
  nextTick(() => {
    isLoveMessageAnimating.value[index] = true;
  });
};

onMounted(() => {
  observer = new IntersectionObserver(checkImageVisibility, {
    root: null,
    rootMargin: '0px',
    threshold: 0.1
  });

  imageContainers.value.forEach((container) => {
    if (container) {
      observer.observe(container);
    }
  });
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>

<style scoped>
.gallery {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px 15px;
  background-color: #ffc0cb;
  color: #fff;
  font-family: 'Arial', sans-serif;
}

h1 {
  font-size: 36px;
  margin-bottom: 30px;
}

.image-container {
  margin-bottom: 60px;
  position: relative;
}

.image {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
  opacity: 0;
}

.fade-in {
  animation: fadeIn 1s ease forwards;
}

.slide-up {
  animation: slideUp 1s ease forwards;
}

.zoom-in {
  animation: zoomIn 1s ease forwards;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideUp {
  from { transform: translateY(50px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

@keyframes zoomIn {
  from { transform: scale(0.8); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}

.love-message {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 24px;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  opacity: 0;
  animation-duration: 6s;
  animation-timing-function: ease;
  animation-fill-mode: forwards;
}

.love-message.animate {
  animation-name: floatMessage;
}

@keyframes floatMessage {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) translateY(20px);
  }
  16.67% {
    opacity: 1;
  }
  83.33% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: translate(-50%, -50%) translateY(-20px);
  }
}

@media (max - width: 480px) {
  h1 {
    font-size: 28px;
  }

  .image-container {
    margin-bottom: 40px;
  }

  .love-message {
    font-size: 18px;
  }
}
</style>
