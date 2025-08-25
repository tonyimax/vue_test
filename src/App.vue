<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

import { ref } from 'vue'

// 声明响应式变量
const count = ref(0)
const message = ref('点击按钮值自增1')
const isActive = ref(false)

// 访问值需要使用 .value
console.log(count.value) // 0
count.value++ // 修改值

// 在模板中自动解包，不需要 .value
// <div>{{ count }}</div>
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/RaspberryPi.png" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="恭喜你，你做到了!" />
      <div id="app">
        <button @click="count++">
          {{message}}: {{ count }}
        </button>
      </div>
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
