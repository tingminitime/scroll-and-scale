
<template>
  <div class="section slogan">
    這台相機，最懂拍出你的型。
  </div>
  <div
    class="section section2"
    :class="{ sticky: fixClass }"
    :style="{ '--scale': progress }"
  >
    <div class="phone">
      <img src="https://picsum.photos/1920/1200?random=1">
      <div class="rect"></div>
    </div>
  </div>
  <div
    class="section section3"
    :class="{ static: fixClass }"
  >
    <div class="phone">
      <img src="https://picsum.photos/1920/1200?random=1">
      <div class="rect"></div>
    </div>
  </div>
  <div class="section slogan">
    這台相機，最懂拍出你的型。
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const progress = ref(0)

/**
 * progress : 3 ~ 1
 * progress 代表 css scale 的值
 */
onMounted(() => {
  const app = document.querySelector('#app')
  app.addEventListener('scroll', function (e) {
    // scrollTop 還在第 1 個區塊 (section1) 之間，progress 不變
    if (app.scrollTop < window.innerHeight) {
      progress.value = 3
    }
    // scrollTop 超過第 3 個區塊 ( section3)，progress 等於 1
    else if (app.scrollTop > window.innerHeight * 2) {
      progress.value = 1
    }
    // scrollTop 在第 2 ~ 3 個區塊，progress 變化
    else {
      // progress
      progress.value = Math.round((3 - 2 * ((app.scrollTop - window.innerHeight) / window.innerHeight)) * 100) / 100
    }
  })
})

// 當卷軸進程還還在 section2 以上，也就是要讓 scale 變動的區間
const fixClass = computed(() => {
  return progress.value > 1
})

</script>

<style lang="sass">
  @import '@/style/sass/app.sass'
  

</style>
