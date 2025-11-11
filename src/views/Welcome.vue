<template>
  <div class="welcome-container">
    <nav class="navbar">
      <div class="nav-content">
        <h2 class="logo">網站名稱</h2>
        <div class="nav-links">
          <router-link to="/welcome" class="nav-link">首頁</router-link>
          <router-link to="/about" class="nav-link">關於我們</router-link>
          <button @click="handleLogout" class="logout-btn">登出</button>
        </div>
      </div>
    </nav>

    <main class="main-content">
      <div class="welcome-card">
        <h1>歡迎回來，{{ username }}！</h1>
        <p class="welcome-message">很高興再次見到您</p>
        <div class="info-section">
          <p>環境：{{ isProduction ? '正式環境' : '測試環境' }}</p>
          <p>Context Path: {{ contextPath }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const username = ref('')
const contextPath = import.meta.env.VITE_CONTEXT_PATH || '/'
const isProduction = import.meta.env.MODE === 'production'

onMounted(() => {
  username.value = localStorage.getItem('username') || '訪客'
})

const handleLogout = () => {
  localStorage.removeItem('isAuthenticated')
  localStorage.removeItem('username')
  router.push('/')
}
</script>

<style scoped lang="scss">
.welcome-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.navbar {
  background: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 16px 0;
}

.nav-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  margin: 0;
  font-size: 24px;
  color: #667eea;
  font-weight: 600;
}

.nav-links {
  display: flex;
  gap: 24px;
  align-items: center;
}

.nav-link {
  color: #555;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;

  &:hover {
    color: #667eea;
  }

  &.router-link-active {
    color: #667eea;
  }
}

.logout-btn {
  padding: 8px 20px;
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 6px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.3s, transform 0.2s;

  &:hover {
    background: #c0392b;
    transform: translateY(-1px);
  }
}

.main-content {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 80px 24px;
}

.welcome-card {
  background: white;
  padding: 64px;
  border-radius: 16px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 600px;

  h1 {
    margin: 0 0 16px 0;
    font-size: 36px;
    color: #333;
  }

  .welcome-message {
    font-size: 18px;
    color: #666;
    margin-bottom: 40px;
  }

  .info-section {
    padding-top: 32px;
    border-top: 1px solid #eee;

    p {
      margin: 8px 0;
      color: #888;
      font-size: 14px;
    }
  }
}
</style>
