<template>
  <div class="about-container">
    <nav class="navbar">
      <div class="nav-content">
        <h2 class="logo">網站名稱</h2>
        <div class="nav-links">
          <router-link v-if="isAuthenticated" to="/welcome" class="nav-link">首頁</router-link>
          <router-link to="/about" class="nav-link">關於我們</router-link>
          <button v-if="isAuthenticated" @click="handleLogout" class="logout-btn">登出</button>
          <router-link v-else to="/" class="login-link">登入</router-link>
        </div>
      </div>
    </nav>

    <main class="main-content">
      <div class="about-section">
        <h1>關於我們</h1>
        <div class="content-card">
          <h2>公司簡介</h2>
          <p>
            我們是一家致力於提供優質服務的專業團隊。憑藉多年的經驗和專業知識，
            我們為客戶提供最佳的解決方案。
          </p>
        </div>

        <div class="content-card">
          <h2>我們的使命</h2>
          <p>
            透過創新技術和專業服務，為客戶創造價值，建立長期合作關係。
            我們相信誠信、專業、創新是成功的關鍵。
          </p>
        </div>

        <div class="content-card">
          <h2>聯絡我們</h2>
          <div class="contact-info">
            <p><strong>電話：</strong>02-1234-5678</p>
            <p><strong>Email：</strong>contact@example.com</p>
            <p><strong>地址：</strong>台北市信義區信義路五段7號</p>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const isAuthenticated = ref(false)

onMounted(() => {
  isAuthenticated.value = localStorage.getItem('isAuthenticated') === 'true'
})

const handleLogout = () => {
  localStorage.removeItem('isAuthenticated')
  localStorage.removeItem('username')
  isAuthenticated.value = false
  router.push('/')
}
</script>

<style scoped lang="scss">
.about-container {
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

.nav-link,
.login-link {
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
  max-width: 1200px;
  margin: 0 auto;
  padding: 80px 24px;
}

.about-section {
  h1 {
    text-align: center;
    font-size: 42px;
    color: #333;
    margin-bottom: 48px;
  }
}

.content-card {
  background: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  margin-bottom: 32px;
  transition: transform 0.3s, box-shadow 0.3s;

  &:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  }

  h2 {
    color: #667eea;
    font-size: 24px;
    margin-bottom: 16px;
  }

  p {
    color: #555;
    font-size: 16px;
    line-height: 1.8;
    margin: 8px 0;
  }

  .contact-info {
    margin-top: 16px;

    p {
      margin: 12px 0;
      font-size: 16px;

      strong {
        color: #333;
      }
    }
  }
}
</style>
