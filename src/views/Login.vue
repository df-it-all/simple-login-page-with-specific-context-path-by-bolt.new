<template>
  <div class="login-container">
    <div class="login-card">
      <h1>登入</h1>
      <form @submit.prevent="handleLogin">
        <div class="form-group">
          <label for="username">帳號</label>
          <input
            id="username"
            v-model="username"
            type="text"
            placeholder="請輸入帳號"
            required
          />
        </div>
        <div class="form-group">
          <label for="password">密碼</label>
          <input
            id="password"
            v-model="password"
            type="password"
            placeholder="請輸入密碼"
            required
          />
        </div>
        <button type="submit" class="login-btn">登入</button>
      </form>
      <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const username = ref('')
const password = ref('')
const errorMessage = ref('')

const handleLogin = () => {
  if (username.value && password.value) {
    localStorage.setItem('isAuthenticated', 'true')
    localStorage.setItem('username', username.value)
    router.push('/welcome')
  } else {
    errorMessage.value = '請輸入帳號和密碼'
  }
}
</script>

<style scoped lang="scss">
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.login-card {
  background: white;
  padding: 48px;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  width: 100%;
  max-width: 400px;

  h1 {
    margin: 0 0 32px 0;
    font-size: 28px;
    color: #333;
    text-align: center;
  }
}

.form-group {
  margin-bottom: 24px;

  label {
    display: block;
    margin-bottom: 8px;
    font-size: 14px;
    font-weight: 500;
    color: #555;
  }

  input {
    width: 100%;
    padding: 12px 16px;
    border: 1px solid #ddd;
    border-radius: 8px;
    font-size: 16px;
    transition: border-color 0.3s;
    box-sizing: border-box;

    &:focus {
      outline: none;
      border-color: #667eea;
    }
  }
}

.login-btn {
  width: 100%;
  padding: 14px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 16px rgba(102, 126, 234, 0.4);
  }

  &:active {
    transform: translateY(0);
  }
}

.error-message {
  margin-top: 16px;
  color: #e74c3c;
  text-align: center;
  font-size: 14px;
}
</style>
