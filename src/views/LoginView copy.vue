<template>
  <main class="flex-grow pt-24 pb-16">
    <div class="container mx-auto px-4 sm:px-6 lg:px-8">
      <div class="max-w-5xl mx-auto">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
          <!-- 左侧图片区域 -->
          <div class="hidden lg:block">
            <div class="rounded-2xl overflow-hidden shadow-xl transform transition-custom hover:scale-[1.02]">
              <img
                src="https://design.gemcoder.com/staticResource/echoAiSystemImages/3212bea5fa4eaa5261000c6f945f6628.png"
                alt="登录界面插图" class="w-full h-full object-cover">
            </div>
          </div>

          <!-- 右侧登录表单 -->
          <div class="bg-white rounded-2xl p-8 card-shadow">
            <div class="text-center mb-8">
              <h1 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-dark mb-2">欢迎回来</h1>
              <p class="text-secondary">请输入您的账号和密码登录</p>
            </div>

            <form @submit.prevent="handleLogin" class="space-y-6">
              <!-- 账号输入 -->
              <div class="space-y-2">
                <label for="username" class="block text-sm font-medium text-gray-700">账号</label>
                <div class="relative">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <i class="fas fa-user text-gray-400"></i>
                  </div>
                  <input type="text" id="username" v-model="formData.username"
                    class="block w-full pl-10 pr-3 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary/50 focus:border-primary transition-custom outline-none"
                    placeholder="请输入账号" required>
                </div>
              </div>

              <!-- 密码输入 -->
              <div class="space-y-2">
                <label for="password" class="block text-sm font-medium text-gray-700">密码</label>
                <div class="relative">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <i class="fas fa-lock text-gray-400"></i>
                  </div>
                  <input :type="showPassword ? 'text' : 'password'" id="password" v-model="formData.password"
                    class="block w-full pl-10 pr-10 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary/50 focus:border-primary transition-custom outline-none"
                    placeholder="请输入密码" required>
                  <button type="button" @click="togglePassword"
                    class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-custom">
                    <i :class="showPassword ? 'fas fa-eye' : 'fas fa-eye-slash'"></i>
                  </button>
                </div>
              </div>

              <!-- 记住我和忘记密码 -->
              <div class="flex items-center justify-between">
                <div class="flex items-center">
                  <input id="remember" v-model="formData.remember" type="checkbox"
                    class="h-4 w-4 text-primary focus:ring-primary/50 border-gray-300 rounded transition-custom">
                  <label for="remember" class="ml-2 block text-sm text-gray-700">记住我</label>
                </div>
                <div class="text-sm">
                  <a href="javascript:void(0);"
                    class="font-medium text-primary hover:text-primary/80 transition-custom">忘记密码?</a>
                </div>
              </div>

              <!-- 登录按钮 -->
              <div>
                <button type="submit" :disabled="isLoading"
                  class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-sm text-sm font-medium text-white bg-gradient-primary hover:opacity-95 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary transition-custom">
                  <span v-if="!isLoading">登录</span>
                  <span v-if="isLoading">登录中...</span>
                </button>
              </div>

              <!-- 分隔线 -->
              <div class="relative">
                <div class="absolute inset-0 flex items-center">
                  <div class="w-full border-t border-gray-300"></div>
                </div>
                <div class="relative flex justify-center text-sm">
                  <span class="px-2 bg-white text-gray-500">其他登录方式</span>
                </div>
              </div>

              <!-- 社交登录 -->
              <div class="grid grid-cols-3 gap-4">
                <button type="button" @click="socialLogin('google')"
                  class="flex justify-center items-center py-3 border border-gray-300 rounded-lg text-gray-700 bg-white hover:bg-gray-50 transition-custom">
                  <i class="fab fa-google text-lg"></i>
                </button>
                <button type="button" @click="socialLogin('facebook')"
                  class="flex justify-center items-center py-3 border border-gray-300 rounded-lg text-gray-700 bg-white hover:bg-gray-50 transition-custom">
                  <i class="fab fa-facebook-f text-lg"></i>
                </button>
                <button type="button" @click="socialLogin('github')"
                  class="flex justify-center items-center py-3 border border-gray-300 rounded-lg text-gray-700 bg-white hover:bg-gray-50 transition-custom">
                  <i class="fab fa-github text-lg"></i>
                </button>
              </div>

              <!-- 注册链接 -->
              <div class="text-center">
                <p class="text-sm text-gray-600">
                  还没有账号? <a href="javascript:void(0);"
                    class="font-medium text-primary hover:text-primary/80 transition-custom">立即注册</a>
                </p>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router'; // 如需路由跳转

// 表单数据
const formData = ref({
  username: '',
  password: '',
  remember: false
});

// 状态管理
const showPassword = ref(false);
const isLoading = ref(false);

// 路由实例
const router = useRouter();

// 切换密码显示状态
const togglePassword = () => {
  showPassword.value = !showPassword.value;
};

// 处理登录表单提交
const handleLogin = async () => {
  try {
    isLoading.value = true;

    // 模拟登录请求
    console.log('登录数据:', formData.value);

    // 实际项目中替换为真实API请求
    await new Promise(resolve => setTimeout(resolve, 1500));

    // 登录成功后的操作
    alert('登录成功！');
    // 示例：跳转到首页
    // router.push('/');
  } catch (error) {
    console.error('登录失败:', error);
    alert('登录失败，请检查账号密码是否正确');
  } finally {
    isLoading.value = false;
  }
};

// 处理社交登录
const socialLogin = (platform) => {
  alert(`即将使用${platform}登录`);
  // 实际项目中添加对应社交平台的登录逻辑
};
</script>

<style scoped>
/* 补充缺失的样式类 */
.text-dark {
  color: #1f2937;
}

.text-secondary {
  color: #6b7280;
}

.card-shadow {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.bg-gradient-primary {
  background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
}

.transition-custom {
  transition: all 0.2s ease-in-out;
}

.focus:ring-primary {
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.3);
}

/* 响应式调整 */
@media (max-width: 1024px) {
  .lg\:grid-cols-2 {
    grid-template-columns: 1fr;
  }

  .hidden.lg\:block {
    display: block;
    margin-bottom: 2rem;
  }
}
</style>