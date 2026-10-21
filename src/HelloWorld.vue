<template>
  <div class="page">
    <!-- 顶部导航 -->
    <header class="nav">
      <div class="logo">MySite</div>
      <nav class="links">
        <a href="#home">首页</a>
        <a href="#features">特性</a>
        <a href="#about">关于</a>
      </nav>
      <button class="nav-btn" @click="showTip = !showTip">
        {{ showTip ? '收起提示' : '点我试试' }}
      </button>
    </header>

    <!-- 提示条 -->
    <div v-if="showTip" class="tip">
      👋 你好！这是一条用 Vue 控制的提示条，点右上角按钮可以收起。
    </div>

    <!-- 大标题区 -->
    <section id="home" class="hero">
      <h1>{{ siteTitle }}</h1>
      <p class="subtitle">{{ subtitle }}</p>
      <div class="hero-actions">
        <button class="primary" @click="count++">点击次数：{{ count }}</button>
        <a class="secondary" href="#features">看看特性 ↓</a>
      </div>
    </section>

    <!-- 特性卡片 -->
    <section id="features" class="features">
      <h2>核心特性</h2>
      <div class="cards">
        <div class="card" v-for="item in features" :key="item.title">
          <div class="icon">{{ item.icon }}</div>
          <h3>{{ item.title }}</h3>
          <p>{{ item.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 关于 -->
    <section id="about" class="about">
      <h2>关于这个页面</h2>
      <p>
        这是用 Vue 3 + Vite 写的一个单页面网站。所有文字、颜色、卡片内容都可以在
        <code>App.vue</code> 里直接改，不需要后端，也不需要数据库。
      </p>
    </section>

    <!-- 页脚 -->
    <footer class="footer">
      <p>© {{ year }} MySite · 用 Vue 搭建</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const siteTitle = ref('用 Vue 做一个属于你的页面')
const subtitle = ref('一个页面，也能把导航、介绍、特性、页脚都装下。')
const count = ref(0)
const showTip = ref(true)
const year = new Date().getFullYear()

const features = ref([
  {
    icon: '⚡',
    title: '快',
    desc: 'Vite 启动和热更新都很快，改完保存，浏览器马上刷新。'
  },
  {
    icon: '🧩',
    title: '组件化',
    desc: '页面可以拆成一块一块，每块单独维护，改起来不互相影响。'
  },
  {
    icon: '📱',
    title: '响应式',
    desc: '同一套代码，在电脑和手机上都能正常显示。'
  }
])
</script>

<style scoped>
/* 全局变量，改颜色很方便 */
.page {
  --bg: #f7f8fc;
  --text: #1f2430;
  --muted: #6b7280;
  --primary: #4f46e5;
  --card: #ffffff;
  --border: #e5e7eb;

  min-height: 100vh;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, 'PingFang SC', 'Microsoft YaHei', sans-serif;
}

/* 导航 */
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 32px;
  background: #fff;
  border-bottom: 1px solid var(--border);
  position: sticky;
  top: 0;
  z-index: 10;
}
.logo {
  font-weight: 700;
  font-size: 20px;
  color: var(--primary);
}
.links {
  display: flex;
  gap: 24px;
}
.links a {
  color: var(--muted);
  text-decoration: none;
  font-size: 14px;
}
.links a:hover {
  color: var(--primary);
}
.nav-btn {
  padding: 8px 14px;
  border: 1px solid var(--border);
  background: #fff;
  border-radius: 8px;
  cursor: pointer;
  font-size: 13px;
}

/* 提示条 */
.tip {
  margin: 16px 32px 0;
  padding: 12px 16px;
  background: #eef2ff;
  color: var(--primary);
  border-radius: 10px;
  font-size: 14px;
}

/* 大标题 */
.hero {
  text-align: center;
  padding: 80px 24px 60px;
}
.hero h1 {
  font-size: 44px;
  margin: 0 0 16px;
  line-height: 1.2;
}
.subtitle {
  color: var(--muted);
  font-size: 18px;
  max-width: 560px;
  margin: 0 auto 32px;
}
.hero-actions {
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
}
.primary {
  padding: 12px 22px;
  background: var(--primary);
  color: #fff;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 15px;
}
.secondary {
  padding: 12px 22px;
  border: 1px solid var(--border);
  border-radius: 10px;
  text-decoration: none;
  color: var(--text);
  font-size: 15px;
  background: #fff;
}

/* 卡片区 */
.features {
  padding: 40px 32px 60px;
  max-width: 1100px;
  margin: 0 auto;
}
.features h2,
.about h2 {
  text-align: center;
  font-size: 28px;
  margin-bottom: 32px;
}
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 28px 22px;
  transition: transform 0.2s, box-shadow 0.2s;
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.06);
}
.icon {
  font-size: 32px;
  margin-bottom: 12px;
}
.card h3 {
  margin: 0 0 8px;
  font-size: 18px;
}
.card p {
  margin: 0;
  color: var(--muted);
  font-size: 14px;
  line-height: 1.6;
}

/* 关于 */
.about {
  max-width: 720px;
  margin: 0 auto;
  padding: 20px 32px 80px;
  text-align: center;
}
.about p {
  color: var(--muted);
  line-height: 1.8;
  font-size: 15px;
}
.about code {
  background: #eef2ff;
  color: var(--primary);
  padding: 2px 6px;
  border-radius: 6px;
  font-size: 13px;
}

/* 页脚 */
.footer {
  text-align: center;
  padding: 24px;
  border-top: 1px solid var(--border);
  color: var(--muted);
  font-size: 13px;
  background: #fff;
}

/* 手机适配 */
@media (max-width: 768px) {
  .nav {
    padding: 14px 16px;
    flex-wrap: wrap;
    gap: 10px;
  }
  .links {
    order: 3;
    width: 100%;
    justify-content: center;
    gap: 18px;
  }
  .hero {
    padding: 50px 20px 40px;
  }
  .hero h1 {
    font-size: 30px;
  }
  .cards {
    grid-template-columns: 1fr;
  }
  .features {
    padding: 30px 20px 40px;
  }
  .tip {
    margin: 12px 16px 0;
  }
}
</style>