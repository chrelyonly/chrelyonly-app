<script setup>
import { ref, computed } from 'vue'
import { Download, Link, Search, Moon, Sunny, ChromeFilled } from '@element-plus/icons-vue'

// 暗黑模式切换
const isDark = ref(false)
const toggleDark = () => {
  isDark.value = !isDark.value
}

// 分类与搜索过滤
const currentCategory = ref('全部')
const searchQuery = ref('')

const categories = ['全部', '移动端', '网络工具', '后端服务', '代理/自动化']

// 示例项目列表
const projects = ref([
  {
    title: '莓莓修仙版PC',
    name: 'chrelyonly_xray_win',
    category: 'PC',
    description: 'net10开发的代理工具(莓莓定制版)',
    tech: ['proxy',"pc"],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
  {
    title: '莓莓修仙版android(红尘炼心)',
    name: 'chrelyonly_xray_android',
    category: 'android',
    description: '基于 Jetpack Compose 开发的代理工具(莓莓定制版)',
    tech: ['proxy',"android"],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
  {
    title: '青少年修仙版',
    name: 'chrelyonly_xray_android',
    category: 'android',
    description: '基于 Jetpack Compose 开发的代理工具(莓莓定制版)',
    tech: ['proxy',"android"],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
  {
    title: 'FRP莓莓定制版android',
    name: 'frp_android',
    category: 'android',
    description: '基于 Jetpack Compose 开发的FRP工具(莓莓定制版)',
    tech: ["android"],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
  {
    title: 'FRP莓莓定制版android',
    name: 'frp_android',
    category: 'android',
    description: '基于 Jetpack Compose 开发的FRP工具(莓莓定制版)',
    tech: ["android"],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
  {
    title: 'Android 音乐播放器(莓莓音乐开心版)',
    name: 'chrelyonly_music_android',
    category: '移动端',
    description: '基于 Jetpack Compose 与 Media3 ExoPlayer 开发的本地/流媒体音乐播放器，支持桌面悬浮歌词、沉浸式 UI 及高性能解码。',
    tech: ['Android', 'Jetpack Compose', 'Kotlin', 'Media3'],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
  {
    title: 'Android 储存(莓莓储存开心版)',
    name: 'chrelyonly_object_android',
    category: '移动端',
    description: '基于 Jetpack Compose 开发的储存桶',
    tech: ['Android', 'Jetpack Compose', 'Kotlin', 'Media3'],
    downloadUrl: '#',
    githubUrl: '#',
    version: 'v1.0.0'
  },
])

// 过滤后的项目列表
const filteredProjects = computed(() => {
  return projects.value.filter(item => {
    const matchCat = currentCategory.value === '全部' || item.category === currentCategory.value
    const matchQuery = item.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        item.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        item.description.toLowerCase().includes(searchQuery.value.toLowerCase())
    return matchCat && matchQuery
  })
})
</script>

<template>
  <div class="glass-page" :class="{ 'dark-theme': isDark }">
    <!-- 动态发光背景光斑 -->
    <div class="bg-glow glow-1"></div>
    <div class="bg-glow glow-2"></div>
    <div class="bg-glow glow-3"></div>

    <!-- 顶部毛玻璃导航 -->
    <header class="glass-navbar">
      <div class="nav-content">
        <div class="brand">
          <el-icon class="brand-icon"><ChromeFilled /></el-icon>
          <span class="brand-name">chrelyonly / Project Hub</span>
        </div>
        <div class="nav-actions">
          <el-button
              circle
              :icon="isDark ? Sunny : Moon"
              class="glass-btn-icon"
              @click="toggleDark"
          />
        </div>
      </div>
    </header>

    <!-- 核心 Hero 展区 -->
    <section class="hero-section">
      <div class="hero-card glass-panel">
        <div class="hero-badge">Strawberry Studio</div>
        <h1>作品与应用下载站</h1>
        <p>专注于全栈开发、网络协议、移动应用与效率工具，全心打造高质量开源组件与可运行构建包。</p>

        <!-- 搜索与筛选栏 -->
        <div class="filter-bar">
          <el-input
              v-model="searchQuery"
              placeholder="搜索项目名称、关键词..."
              :prefix-icon="Search"
              clearable
              class="glass-input"
          />
          <div class="category-tags">
            <span
                v-for="cat in categories"
                :key="cat"
                class="cat-item"
                :class="{ active: currentCategory === cat }"
                @click="currentCategory = cat"
            >
              {{ cat }}
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- 项目卡片列表（使用 CSS Grid 解决换行与对齐问题） -->
    <main class="main-container">
      <div class="projects-grid" v-if="filteredProjects.length > 0">
        <div
            v-for="(item, index) in filteredProjects"
            :key="index"
            class="glass-card"
        >
          <div class="card-top">
            <div class="card-header">
              <h3 class="project-title">{{ item.title }}</h3>
              <span class="category-badge">{{ item.category }}</span>
            </div>
            <div class="project-meta">
              <code class="project-name">{{ item.name }}</code>
              <span class="version-tag">{{ item.version }}</span>
            </div>
            <p class="project-desc">{{ item.description }}</p>
          </div>

          <div class="card-bottom">
            <div class="tech-stack">
              <span v-for="(t, tIdx) in item.tech" :key="tIdx" class="tech-chip">
                {{ t }}
              </span>
            </div>
            <div class="card-actions">
              <a :href="item.downloadUrl" class="glass-btn primary">
                <el-icon><Download /></el-icon> 下载应用
              </a>
              <a :href="item.githubUrl" target="_blank" class="glass-btn outline">
                <el-icon><Link /></el-icon> 源码
              </a>
            </div>
          </div>
        </div>
      </div>

      <div v-else class="empty-state glass-panel">
        <p>没有找到相关项目</p>
      </div>
    </main>

    <!-- 页脚 -->
    <footer class="footer-section">
      <p>© 2026 chrelyonly.cn · Built with Vue 3 & Element Plus</p>
    </footer>
  </div>
</template>

<style scoped>
/* ================= 全局毛玻璃与变量 ================= */
.glass-page {
  --bg-color: #f0f4f8;
  --text-primary: #1f2937;
  --text-secondary: #4b5563;
  --glass-bg: rgba(255, 255, 255, 0.45);
  --glass-border: rgba(255, 255, 255, 0.6);
  --glass-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.08);
  --accent-color: #6366f1;
  --accent-hover: #4f46e5;
  --chip-bg: rgba(255, 255, 255, 0.6);

  position: relative;
  min-height: 100vh;
  background-color: var(--bg-color);
  color: var(--text-primary);
  transition: all 0.3s ease;
  overflow-x: hidden;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}

.glass-page.dark-theme {
  --bg-color: #0f172a;
  --text-primary: #f8fafc;
  --text-secondary: #94a3b8;
  --glass-bg: rgba(30, 41, 59, 0.55);
  --glass-border: rgba(255, 255, 255, 0.1);
  --glass-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
  --chip-bg: rgba(255, 255, 255, 0.08);
}

/* 动态背景光斑 */
.bg-glow {
  position: absolute;
  border-radius: 50%;
  filter: blur(90px);
  z-index: 0;
  pointer-events: none;
}
.glow-1 {
  width: 400px;
  height: 400px;
  background: rgba(99, 102, 241, 0.35);
  top: -100px;
  left: -100px;
}
.glow-2 {
  width: 500px;
  height: 500px;
  background: rgba(236, 72, 153, 0.25);
  top: 30%;
  right: -150px;
}
.glow-3 {
  width: 450px;
  height: 450px;
  background: rgba(14, 165, 233, 0.3);
  bottom: 0;
  left: 20%;
}

.glass-panel {
  background: var(--glass-bg);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid var(--glass-border);
  box-shadow: var(--glass-shadow);
  border-radius: 16px;
}

/* ================= 导航栏 ================= */
.glass-navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--glass-bg);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--glass-border);
  padding: 12px 24px;
}
.nav-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.brand {
  display: flex;
  align-items: center;
  gap: 10px;
}
.brand-icon {
  font-size: 24px;
  color: var(--accent-color);
}
.brand-name {
  font-weight: 700;
  font-size: 1.1rem;
}

/* ================= Hero 区域 ================= */
.hero-section {
  position: relative;
  z-index: 1;
  max-width: 1200px;
  margin: 30px auto;
  padding: 0 20px;
}
.hero-card {
  padding: 40px;
  text-align: center;
}
.hero-badge {
  display: inline-block;
  padding: 4px 14px;
  background: rgba(99, 102, 241, 0.15);
  color: var(--accent-color);
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
  margin-bottom: 12px;
}
.hero-card h1 {
  font-size: 2.2rem;
  margin: 10px 0;
  font-weight: 800;
}
.hero-card p {
  color: var(--text-secondary);
  max-width: 650px;
  margin: 0 auto 30px;
  line-height: 1.6;
}

.filter-bar {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  max-width: 600px;
  margin: 0 auto;
}
.glass-input {
  width: 100%;
}
.glass-input :deep(.el-input__wrapper) {
  background: var(--chip-bg);
  backdrop-filter: blur(10px);
  border-radius: 12px;
  box-shadow: none;
  border: 1px solid var(--glass-border);
}
.category-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
}
.cat-item {
  padding: 6px 16px;
  border-radius: 20px;
  font-size: 0.85rem;
  cursor: pointer;
  background: var(--chip-bg);
  border: 1px solid var(--glass-border);
  transition: all 0.2s ease;
  color: var(--text-secondary);
}
.cat-item.active, .cat-item:hover {
  background: var(--accent-color);
  color: #ffffff;
  border-color: var(--accent-color);
}

/* ================= CSS Grid 瀑布网格布局 ================= */
.main-container {
  position: relative;
  z-index: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 24px;
}

.glass-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 24px;
  background: var(--glass-bg);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid var(--glass-border);
  box-shadow: var(--glass-shadow);
  border-radius: 16px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.glass-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 16px 36px rgba(0, 0, 0, 0.12);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}
.project-title {
  font-size: 1.15rem;
  margin: 0;
  font-weight: 700;
}
.category-badge {
  font-size: 0.75rem;
  padding: 2px 8px;
  border-radius: 6px;
  background: rgba(99, 102, 241, 0.15);
  color: var(--accent-color);
}
.project-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
}
.project-name {
  font-family: monospace;
  font-size: 0.82rem;
  opacity: 0.8;
}
.version-tag {
  font-size: 0.75rem;
  color: var(--text-secondary);
}
.project-desc {
  font-size: 0.9rem;
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 20px;
}

.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 20px;
}
.tech-chip {
  font-size: 0.75rem;
  padding: 3px 8px;
  border-radius: 6px;
  background: var(--chip-bg);
  border: 1px solid var(--glass-border);
}
.card-actions {
  display: flex;
  gap: 10px;
}
.glass-btn {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  padding: 8px 12px;
  border-radius: 8px;
  font-size: 0.85rem;
  text-decoration: none;
  font-weight: 500;
  transition: all 0.2s ease;
}
.glass-btn.primary {
  background: var(--accent-color);
  color: white;
}
.glass-btn.primary:hover {
  background: var(--accent-hover);
}
.glass-btn.outline {
  background: var(--chip-bg);
  color: var(--text-primary);
  border: 1px solid var(--glass-border);
}
.glass-btn.outline:hover {
  background: var(--glass-border);
}

.empty-state {
  text-align: center;
  padding: 40px;
  color: var(--text-secondary);
}

.footer-section {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 30px 0;
  color: var(--text-secondary);
  font-size: 0.85rem;
}
</style>