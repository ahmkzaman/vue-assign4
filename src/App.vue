<script setup>
import { ref } from 'vue';

const images = ref([
 'https://images.unsplash.com/photo-1517649763962-0c623066013b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
  'https://images.unsplash.com/photo-1594911772125-07fc7a2d8d9f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
  'https://images.unsplash.com/photo-1622629797619-c100e3e67e2e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1031&q=80',
  'https://images.unsplash.com/photo-1560884854-6c1de51e4e15?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
  'https://images.unsplash.com/photo-1601259406831-74d661a0475a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
  'https://images.unsplash.com/photo-1513221191397-544071c48f2c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80'
]);

const activeImageIndex = ref(0);
const slideInterval = 3000; 
let intervalId = null;

function getCurrentImage() {
  return images.value[activeImageIndex.value];
}

function nextImage() {
  activeImageIndex.value = (activeImageIndex.value + 1) % images.value.length;
}

function prevImage() {
  activeImageIndex.value =
    (activeImageIndex.value - 1 + images.value.length) % images.value.length;
}

function startAutoSlide() {
  intervalId = setInterval(() => {
    nextImage();
  }, slideInterval);
}

function stopAutoSlide() {
  clearInterval(intervalId);
}

startAutoSlide();
</script>


<template>
<section>
  <div class="text-center mt-6">
  <h2 class="text-4xl font-extrabold text-red-600">
    <span class="bg-gradient-to-r from-red-500 to-pink-500 text-transparent bg-clip-text">Image Carousel by Vue.js 3</span>
  </h2>
</div>

 <div class="max-w-400px mx-auto mt-4">
    <div class="carousel-container aspect-h-2 h-96">
      <div class="image-container" v-for="(image, index) in images" :key="index" v-show="activeImageIndex === index">
        <div class="image-item mt-4">
          <button class="prev-btn" @click="prevImage">&lt;</button>
          <img :src="image" alt="Carousel Image" class="img-size rounded" />
          <button class="next-btn" @click="nextImage">&gt;</button>
        </div>
      </div>
    </div>
  </div>
</section>

<section>

  <div class="max-w-400px mx-auto">
      <div class="carousel-container aspect-h-2 h-96">
        <div class="image-container-all mt-2">
          <div class="image-item-all" v-for="(image, index) in images" :key="index" :class="{ 'highlighted': activeImageIndex === index }">
            <img :src="image" alt="Carousel Image" class="rounded border-4 border-red-600" />
          </div>
        </div>
      </div>
    </div>
</section>

</template>


<style scoped>
.carousel-container {
  overflow: hidden;
  position: relative;
}

.image-item {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  left: 0;
  height: 100%;
  width: 100%;
  transition: transform 0.2s ease-in-out;
}
.image-item:not(:first-child) {
  transform: translateX(-100%);
}
.img-size{
  height: 31.25rem;
  width: 62rem;
}
.image-container {
  position: relative; 
}
.prev-btn,
.next-btn {
  position: absolute;
  margin-bottom: 5%;
  transform: translateY(-50%);
  font-size: 30px;
  color: rgb(202, 11, 11);
  background-color: rgba(239, 235, 235, 0.5);
  border: none;
  cursor: pointer;
  border-radius: 50%; 
  width: 60px; 
  height: 60px; 
  display: flex;
  justify-content: center;
  align-items: center;
}

.prev-btn,
.next-btn {
  z-index: 1; 
}
.prev-btn{
  margin-right: 60%;
}
.next-btn{
  margin-left: 60%;
}

/* for bottom slider */
.image-container-all {
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  width: 100%;
  height: 60%;
}

.image-item-all {
  flex: 0 0 auto;
  margin-left: 25px;
  transition: transform 0.3s ease-in-out;
  filter: blur(2px); 
  width: 6.5rem; 
  height: 6rem; 
}

.highlighted {
  transform: scale(1.2); 
  filter: blur(0); 
}

.image-item-all img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

</style>
