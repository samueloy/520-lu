<template>
  <div class="home">
    <div class="heart-container">
      <div class="heart">
        <span class="name">路雪梅</span>
      </div>
    </div>
    <h1>亲爱的，520快乐！</h1>
    <p>在这个特别的日子，我想对你说...</p>
    <button @click="handleClick" class="lovely-button">{{ buttonText }}</button>
    <transition name="fade">
      <div v-if="showPopup" class="lovely-popup" @click="handlePopupClick">
        <p>{{ currentMessage }}</p>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

// 爱意满满的情话列表
const loveMessages = ref([
  '你是我生命中最璀璨的星光，照亮我前行的每一步。',
  '自从遇到你，我的世界充满了温暖与甜蜜，余生我想一直陪伴在你身边。',
  '在这纷繁复杂的世界里，你是我内心最柔软的牵挂，爱你永不止息。',
  '无论在什么地方，你都是我最温暖的依靠，让我在每一个时刻都感到幸福。',
]);

// 当前显示的情话索引
const messageIndex = ref(-1);
// 按钮显示的文本
const buttonText = ref('点击倾听我的爱意');
// 是否显示弹窗
const showPopup = ref(false);
// 当前显示的情话
const currentMessage = ref('');

const handleClick = () => {
  if (messageIndex.value < loveMessages.value.length - 1) {
    messageIndex.value++;
    currentMessage.value = loveMessages.value[messageIndex.value];
    showPopup.value = true;
    buttonText.value = '继续倾听';
  } else {
    router.push('/gallery');
  }
};

const handlePopupClick = () => {
  if (messageIndex.value < loveMessages.value.length - 1) {
    messageIndex.value++;
    currentMessage.value = loveMessages.value[messageIndex.value];
  } else {
    showPopup.value = false;
    router.push('/gallery');
  }
};
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #ffc0cb;
  color: #fff;
  font-family: 'Arial', sans-serif;
  /* padding: 0 15px; */
  box-sizing: border-box;
}

.heart-container {
  /* position: relative; */
  width: 100%;
  /* 进一步减少底部外边距，让爱心上移 */
  /* margin-bottom: -60px;  */
  height: 180px; /* 增加容器高度以适应更大的爱心 */
}

.heart {
  position: absolute;
  top: 25%;
  left: calc(50% - 70px);
  transform: translate(-50%, -50%);
  /* 增大爱心尺寸 */
  width: 180px; 
  height: 180px; 
  background-color: #ff4444;
  transform: rotate(-45deg) translate(-50%, -50%);
  animation: heartbeat 1.5s infinite;
}

.heart::before,
.heart::after {
  content: "";
  position: absolute;
  /* 增大伪元素尺寸 */
  width: 180px; 
  height: 180px; 
  background-color: #ff4444;
  border-radius: 50%;
}

.heart::before {
  /* 调整伪元素位置 */
  top: -90px; 
  left: 0;
}

.heart::after {
  /* 调整伪元素位置 */
  left: 90px; 
  top: 0;
}

.name {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) rotate(45deg);
  color: white;
  /* 增大名字字体大小 */
  font-size: 24px; 
  font-weight: bold;
  z-index: 1;
}

@keyframes heartbeat {
  0% {
    transform: rotate(-45deg) scale(1);
  }
  25% {
    transform: rotate(-45deg) scale(1.1);
  }
  50% {
    transform: rotate(-45deg) scale(1);
  }
  75% {
    transform: rotate(-45deg) scale(1.1);
  }
  100% {
    transform: rotate(-45deg) scale(1);
  }
}

h1 {
  font-size: 36px;
  margin-bottom: 15px;
}

p {
  font-size: 18px;
  margin-bottom: 30px;
}

.lovely-button {
  padding: 15px 30px;
  font-size: 18px;
  background-color: #ff69b4;
  color: white;
  border: none;
  border-radius: 25px;
  box-shadow: 0 5px 15px rgba(255, 105, 180, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
}

.lovely-button:hover {
  background-color: #ff1493;
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(255, 105, 180, 0.5);
}

.lovely-popup {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff0f5;
  padding: 30px;
  border-radius: 20px;
  color: #ff1493;
  max-width: 80%;
  text-align: center;
  box-shadow: 0 10px 30px rgba(255, 105, 180, 0.3);
  cursor: pointer;
  font-family: 'Comic Sans MS', cursive;
}

.lovely-popup p {
  font-size: 20px;
  margin: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 480px) {
  h1 {
    font-size: 28px;
  }

  p {
    font-size: 16px;
  }

  .lovely-button {
    padding: 12px 24px;
    font-size: 16px;
  }

  .heart {
    /* 小屏幕下调整爱心尺寸 */
    width: 120px; 
    height: 120px;
  }

  .heart::before,
  .heart::after {
    /* 小屏幕下调整伪元素尺寸 */
    width: 120px; 
    height: 120px;
  }

  .heart::before {
    /* 小屏幕下调整伪元素位置 */
    top: -60px; 
  }

  .heart::after {
    /* 小屏幕下调整伪元素位置 */
    left: 60px; 
  }

  .name {
    /* 小屏幕下调整名字字体大小 */
    font-size: 18px; 
  }

  .lovely-popup {
    padding: 20px;
    font-size: 16px;
  }
}
</style>
