<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

import { ref,onMounted } from 'vue'
import axios from 'axios';

// 声明响应式变量
const count = ref(0)
const message = ref('点击按钮值自增1')
const isActive = ref(false)

// 访问值需要使用 .value
console.log(count.value) // 0
count.value++ // 修改值

const clientIp=ref("正在获取IP...");

defineProps({
  ip_field: {
    type: String,
    required: true,
  },
})
// 在模板中自动解包，不需要 .value
// <div>{{ count }}</div>

const getIp = async () => {
  try {
    const response = await axios.get('/ip');
    clientIp.value = response.data.ip;
    document.title="网站来自:"+clientIp.value;
    console.log(clientIp.value);
  } catch (error) {
    console.error('获取IP失败:', error);
    clientIp.value = '获取失败';
  }
}



// 生命周期钩子
onMounted(() => {
  getIp();
});

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/RaspberryPi.png" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld v-bind:msg="'服务器IP:'+clientIp" />
      <hello-world :msg="clientIp" />

      <p>服务器IP：{{ clientIp }}</p>
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
